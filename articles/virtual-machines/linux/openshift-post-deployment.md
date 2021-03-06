---
title: Azure의 OpenShift 배포 후 작업 | Microsoft Docs
description: OpenShift 클러스터가 배포 된 후 추가 작업입니다.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: haroldwongms
manager: joraio
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/02/2019
ms.author: haroldw
ms.openlocfilehash: bc7a49aa143400387afcd59d5b9307d82a028486
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58098664"
---
# <a name="post-deployment-tasks"></a>배포 후 작업

OpenShift 클러스터를 배포한 후에는 추가 항목을 구성할 수 있습니다. 이 문서에서는 다음 내용을 설명합니다.

- Azure AD(Azure Active Directory)를 사용하여 Single Sign-On을 구성하는 방법
- OpenShift를 모니터링 하려면 Azure Monitor 로그를 구성 하는 방법
- 메트릭 및 로깅을 구성하는 방법
- OSBA(Open Service Broker for Azure)를 설치하는 방법

## <a name="configure-single-sign-on-by-using-azure-active-directory"></a>Azure Active Directory를 사용하여 Single Sign-On 구성

Azure Active Directory를 인증에 사용하려면 먼저 Azure AD 앱 등록을 만들어야 합니다. 이 과정에는 앱 등록 만들기 및 권한 구성이라는 두 가지 단계가 포함됩니다.

### <a name="create-an-app-registration"></a>앱 등록 만들기

이 단계에서는 Azure CLI를 사용하여 앱 등록을 만들고 GUI(포털)를 사용하여 권한을 설정합니다. 앱 등록을 만들려면 다음 5가지 정보가 필요합니다.

- 표시 이름: 앱 등록 이름 (예: OCPAzureAD)
- 홈 페이지: OpenShift 콘솔 URL (예: https://masterdns343khhde.westus.cloudapp.azure.com/console)
- 식별자 URI: OpenShift 콘솔 URL (예: https://masterdns343khhde.westus.cloudapp.azure.com/console)
- 회신 URL: 마스터 공용 URL 및 앱 등록 이름 (예를 들어, https://masterdns343khhde.westus.cloudapp.azure.com/oauth2callback/OCPAzureAD)
- 암호: 보안 암호 (강력한 암호 사용)

다음 예에서는 위 정보를 사용하여 앱 등록을 만듭니다.

```azurecli
az ad app create --display-name OCPAzureAD --homepage https://masterdns343khhde.westus.cloudapp.azure.com/console --reply-urls https://masterdns343khhde.westus.cloudapp.azure.com/oauth2callback/hwocpadint --identifier-uris https://masterdns343khhde.westus.cloudapp.azure.com/console --password {Strong Password}
```

명령이 성공하면 다음과 유사한 JSON 출력이 표시됩니다.

```json
{
  "appId": "12345678-ca3c-427b-9a04-ab12345cd678",
  "appPermissions": null,
  "availableToOtherTenants": false,
  "displayName": "OCPAzureAD",
  "homepage": "https://masterdns343khhde.westus.cloudapp.azure.com/console",
  "identifierUris": [
    "https://masterdns343khhde.westus.cloudapp.azure.com/console"
  ],
  "objectId": "62cd74c9-42bb-4b9f-b2b5-b6ee88991c80",
  "objectType": "Application",
  "replyUrls": [
    "https://masterdns343khhde.westus.cloudapp.azure.com/oauth2callback/OCPAzureAD"
  ]
}
```

이후 단계를 위해 명령에서 반환되는 appId 속성을 기록해 둡니다.

Azure Portal에서 다음을 수행합니다.

1. **Azure Active Directory** > **앱 등록**을 선택합니다.
2. 앱 등록(예: OCPAzureAD)을 검색합니다.
3. 결과에서 앱 등록을 클릭합니다.
4. **설정**에서 **필요한 권한**을 선택합니다.
5. **필요한 권한**에서 **추가**를 선택합니다.

   ![앱 등록](media/openshift-post-deployment/app-registration.png)

6. 1 단계를 클릭 합니다. API를 선택한 다음 클릭 **Windows Azure Active Directory (Microsoft.Azure.ActiveDirectory)** 합니다. 아래쪽에서 **선택**을 선택합니다.

   ![앱 등록 API 선택](media/openshift-post-deployment/app-registration-select-api.png)

7. 2 단계: 권한 선택 **로그인 및 사용자 프로필 읽기** 아래에서 **위임 된 권한**를 클릭 하 고 **선택**합니다.

   ![앱 등록 액세스](media/openshift-post-deployment/app-registration-access.png)

8. **완료**를 선택합니다.

### <a name="configure-openshift-for-azure-ad-authentication"></a>Azure AD 인증을 위한 OpenShift 구성

Azure AD를 인증 공급자로 사용하도록 OpenShift를 구성하려면 모든 마스터 노드에서 /etc/origin/master/master-config.yaml 파일을 편집해야 합니다.

다음 CLI 명령을 사용하여 테넌트 ID를 찾습니다.

```azurecli
az account show
```

yaml 파일에서 다음 줄을 찾습니다.

```yaml
oauthConfig:
  assetPublicURL: https://masterdns343khhde.westus.cloudapp.azure.com/console/
  grantConfig:
    method: auto
  identityProviders:
  - challenge: true
    login: true
    mappingMethod: claim
    name: htpasswd_auth
    provider:
      apiVersion: v1
      file: /etc/origin/master/htpasswd
      kind: HTPasswdPasswordIdentityProvider
```

이전 줄 바로 뒤에 다음 줄을 삽입합니다.

```yaml
  - name: <App Registration Name>
    challenge: false
    login: true
    mappingMethod: claim
    provider:
      apiVersion: v1
      kind: OpenIDIdentityProvider
      clientID: <appId>
      clientSecret: <Strong Password>
      claims:
        id:
        - sub
        preferredUsername:
        - unique_name
        name:
        - name
        email:
        - email
      urls:
        authorize: https://login.microsoftonline.com/<tenant Id>/oauth2/authorize
        token: https://login.microsoftonline.com/<tenant Id>/oauth2/token
```

identityProviders 아래의 텍스트가 제대로 정렬되어 있는지 확인합니다. 다음 CLI 명령을 사용하여 테넌트 ID를 찾습니다. ```az account show```

모든 마스터 노드에서 OpenShift 마스터 서비스를 다시 시작합니다.

**여러 마스터가 있는 OCP(OpenShift Container Platform)**

```bash
sudo systemctl restart atomic-openshift-master-api
sudo systemctl restart atomic-openshift-master-controllers
```

**단일 마스터가 있는 OpenShift Container Platform**

```bash
sudo systemctl restart atomic-openshift-master
```

**여러 마스터가 있는 OKD**

```bash
sudo systemctl restart origin-master-api
sudo systemctl restart origin-master-controllers
```

**단일 마스터가 있는 OKD**

```bash
sudo systemctl restart origin-master
```

OpenShift 콘솔에 htpasswd_auth 및 [앱 등록]이라는 두 가지 인증 옵션이 표시됩니다.

## <a name="monitor-openshift-with-azure-monitor-logs"></a>Azure Monitor 로그로 OpenShift를 모니터링 합니다.

OpenShift에 Log Analytics 에이전트를 추가하는 방법에는 세 가지가 있습니다.
- 각 OpenShift 노드에 직접 Linux용 Log Analytics 에이전트 설치
- 각 OpenShift 노드에서 Azure 모니터 VM 확장을 사용 하도록 설정
- OpenShift 디먼 집합으로 Log Analytics 에이전트 설치

전체 지침은 https://docs.microsoft.com/azure/log-analytics/log-analytics-containers#configure-a-log-analytics-agent-for-red-hat-openshift에 나와 있습니다.

## <a name="configure-metrics-and-logging"></a>메트릭 및 로깅 구성

분기에 따라, OpenShift Container Platform 및 OKD용 Azure Resource Manager 템플릿은 설치의 일부로 메트릭 및 로깅을 사용하도록 설정하기 위한 입력 매개 변수를 제공할 수 있습니다.

또한 OpenShift Container Platform Marketplace 제품은 클러스터 설치 동안 메트릭 및 로깅을 사용하도록 설정하기 위한 옵션도 제공합니다.

클러스터를 설치하는 동안 메트릭/로깅을 사용하도록 설정하지 않으면 사후에 쉽게 사용하도록 설정할 수 있습니다.

### <a name="ansible-inventory-pre-work"></a>Ansible 인벤토리 사전 작업

Ansible 인벤토리 파일(/etc/ansible/hosts)에 메트릭/로깅에 대한 적절한 변수가 있는지 확인합니다. 인벤토리 파일은 사용되는 템플릿을 기준으로 서로 다른 호스트에서 찾을 수 있습니다.

OpenShift Container 템플릿 및 Marketplace 제품의 경우 인벤토리 파일이 Bastion 호스트에 있습니다. OKD 템플릿의 경우 인벤토리 파일은 사용 중인 분기를 기준으로 마스터 0 호스트 또는 bastion 호스트에 있습니다.

1. /etc/ansible/hosts 파일을 편집하고 ID 공급자 섹션 뒤에 다음 줄을 추가합니다(# Enable HTPasswdPasswordIdentityProvider). 이러한 줄이 이미 있으면 다시 추가하지 마세요.

   OpenShift / OKD 버전 3.9 및 이전 버전

   ```yaml
   # Setup metrics
   openshift_hosted_metrics_deploy=false
   openshift_metrics_cassandra_storage_type=dynamic
   openshift_metrics_start_cluster=true
   openshift_metrics_hawkular_nodeselector={"type":"infra"}
   openshift_metrics_cassandra_nodeselector={"type":"infra"}
   openshift_metrics_heapster_nodeselector={"type":"infra"}
   openshift_hosted_metrics_public_url=https://metrics.$ROUTING/hawkular/metrics

   # Setup logging
   openshift_hosted_logging_deploy=false
   openshift_hosted_logging_storage_kind=dynamic
   openshift_logging_fluentd_nodeselector={"logging":"true"}
   openshift_logging_es_nodeselector={"type":"infra"}
   openshift_logging_kibana_nodeselector={"type":"infra"}
   openshift_logging_curator_nodeselector={"type":"infra"}
   openshift_master_logging_public_url=https://kibana.$ROUTING
   ```

   OpenShift / OKD 버전 3.10 이상

   ```yaml
   # Setup metrics
   openshift_metrics_install_metrics=false
   openshift_metrics_start_cluster=true
   openshift_metrics_hawkular_nodeselector={"node-role.kubernetes.io/infra":"true"}
   openshift_metrics_cassandra_nodeselector={"node-role.kubernetes.io/infra":"true"}
   openshift_metrics_heapster_nodeselector={"node-role.kubernetes.io/infra":"true"}

   # Setup logging
   openshift_logging_install_logging=false
   openshift_logging_fluentd_nodeselector={"logging":"true"}
   openshift_logging_es_nodeselector={"node-role.kubernetes.io/infra":"true"}
   openshift_logging_kibana_nodeselector={"node-role.kubernetes.io/infra":"true"}
   openshift_logging_curator_nodeselector={"node-role.kubernetes.io/infra":"true"}
   openshift_logging_master_public_url=https://kibana.$ROUTING
   ```

3. 동일한 /etc/ansible/hosts 파일에서 $ROUTING을 openshift_master_default_subdomain 옵션에 사용된 문자열로 대체합니다.

### <a name="azure-cloud-provider-in-use"></a>사용 중인 Azure Cloud Provider

배포 중에 제공된 자격 증명을 사용하여 bastion 노드 또는 첫 번째 마스터 노드(사용 중인 템플릿 및 분기에 따라)에 대해 SSH를 수행합니다. 다음 명령을 실행합니다.

**OpenShift Container Platform 3.7 이하**

```bash
ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/byo/openshift-cluster/openshift-metrics.yml \
-e openshift_metrics_install_metrics=True \
-e openshift_metrics_cassandra_storage_type=dynamic

ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/byo/openshift-cluster/openshift-logging.yml \
-e openshift_logging_install_logging=True \
-e openshift_hosted_logging_storage_kind=dynamic
```

**OpenShift Container Platform 3.9 이상**

```bash
ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/openshift-metrics/config.yml \
-e openshift_metrics_install_metrics=True \
-e openshift_metrics_cassandra_storage_type=dynamic

ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/openshift-logging/config.yml \
-e openshift_logging_install_logging=True \
-e openshift_logging_es_pvc_dynamic=true
```

**OKD 3.7 이하**

```bash
ansible-playbook ~/openshift-ansible/playbooks/byo/openshift-cluster/openshift-metrics.yml \
-e openshift_metrics_install_metrics=True \
-e openshift_metrics_cassandra_storage_type=dynamic

ansible-playbook ~/openshift-ansible/playbooks/byo/openshift-cluster/openshift-logging.yml \
-e openshift_logging_install_logging=True \
-e openshift_hosted_logging_storage_kind=dynamic
```

**OKD 3.9 이상**

```bash
ansible-playbook ~/openshift-ansible/playbooks/byo/openshift-cluster/openshift-metrics.yml \
-e openshift_metrics_install_metrics=True \
-e openshift_metrics_cassandra_storage_type=dynamic

ansible-playbook ~/openshift-ansible/playbooks/openshift-logging/config.yml \
-e openshift_logging_install_logging=True \
-e openshift_logging_es_pvc_dynamic=true
```

### <a name="azure-cloud-provider-not-in-use"></a>사용되지 않는 Azure Cloud Provider

배포 중에 제공된 자격 증명을 사용하여 bastion 노드 또는 첫 번째 마스터 노드(사용 중인 템플릿 및 분기에 따라)에 대해 SSH를 수행합니다. 다음 명령을 실행합니다.


**OpenShift Container Platform 3.7 이하**

```bash
ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/byo/openshift-cluster/openshift-metrics.yml \
-e openshift_metrics_install_metrics=True

ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/byo/openshift-cluster/openshift-logging.yml \
-e openshift_logging_install_logging=True
```

**OpenShift Container Platform 3.9 이상**

```bash
ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/openshift-metrics/config.yml \
-e openshift_metrics_install_metrics=True

ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/openshift-logging/config.yml \
-e openshift_logging_install_logging=True
```

**OKD 3.7 이하**

```bash
ansible-playbook ~/openshift-ansible/playbooks/byo/openshift-cluster/openshift-metrics.yml \
-e openshift_metrics_install_metrics=True

ansible-playbook ~/openshift-ansible/playbooks/byo/openshift-cluster/openshift-logging.yml \
-e openshift_logging_install_logging=True
```

**OKD 3.9 이상**

```bash
ansible-playbook ~/openshift-ansible/playbooks/byo/openshift-cluster/openshift-metrics.yml \
-e openshift_metrics_install_metrics=True
ansible-playbook ~/openshift-ansible/playbooks/openshift-logging/config.yml \
-e openshift_logging_install_logging=True
```

## <a name="install-open-service-broker-for-azure-osba"></a>OSBA(Open Service Broker for Azure) 설치

Open Service Broker for Azure 또는 OSBA를 사용하여 OpenShift에서 직접 Azure Cloud Services를 프로비전할 수 있습니다. OSBA는 Azure에서 구현된 Open Service Broker API입니다. Open Service Broker API는 클라우드 기본 애플리케이션이 잠금 없이 클라우드 서비스를 관리하는 데 사용할 수 있는 클라우드 공급자에 대한 공용 언어를 정의하는 사양입니다.

OpenShift에 OSBA를 설치하려면 https://github.com/Azure/open-service-broker-azure#openshift-project-template의 지침을 따르세요. 

## <a name="next-steps"></a>다음 단계

- [OpenShift Container Platform 시작](https://docs.openshift.com/container-platform)
- [OKD 시작](https://docs.okd.io/latest)

---
title: Azure 활동 로그 보관
description: Azure 활동 로그를 저장소 계정에 보관하면 오래 보관할 수 있습니다.
author: nkiest
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 02/22/2019
ms.author: nikiest
ms.subservice: logs
ms.openlocfilehash: 5328173090bce3e3adf51a1503e18c8da5532b0e
ms.sourcegitcommit: 3f4ffc7477cff56a078c9640043836768f212a06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57310908"
---
# <a name="archive-the-azure-activity-log"></a>Azure 활동 로그 보관
이 문서에서는 Azure 포털, PowerShell Cmdlet 또는 플랫폼 간 CLI를 사용하여 저장소 계정에서 [**Azure 활동 로그**](../../azure-monitor/platform/activity-logs-overview.md)를 보관하는 방법을 보여 줍니다. 이 옵션은 감사, 정적 분석 또는 백업을 위해 활동 로그를 90일 이상(보존 정책에 대해 모든 권한으로) 유지하려는 경우에 유용합니다. 90일 이내로 이벤트를 보관해야 하는 경우 활동 로그는 보관 활성화 없이 Azure 플랫폼에 90일 동안 보관되므로 저장소 계정에 보관을 설정할 필요가 없습니다.

> [!WARNING]
> 저장소 계정에서 로그 데이터의 형식이 2018년 11월 1일에 JSON 줄로 변경됩니다. [새 형식을 처리하도록 도구를 업데이트하는 방법과 영향에 대한 설명은 이 아티클을 참조하세요.](./../../azure-monitor/platform/diagnostic-logs-append-blobs.md) 
>
> 

## <a name="prerequisites"></a>필수 조건
시작하기 전에 활동 로그를 보관하려면 [저장소 계정을 만들](../../storage/common/storage-quickstart-create-account.md) 어야 합니다. 모니터링 데이터에 대한 액세스를 보다 잘 제어할 수 있도록 다른 비 모니터링 데이터가 저장된 기존 저장소 계정을 사용하지 않는 것이 좋습니다. 그러나 저장소 계정에 대한 진단 로그 및 메트릭을 보관하는 경우 중앙 위치에서 모든 모니터링 데이터를 유지하도록 활동 로그에 대해 해당 저장소 계정을 사용하는 것이 합리적일 수 있습니다. 설정을 구성하는 사용자가 두 구독에 대한 적절한 RBAC 액세스를 가진 경우 저장소 계정은 로그를 내보내는 구독과 동일한 구독을 가지고 있지 않아도 됩니다.

## <a name="log-profile"></a>로그 프로필
다음 방법 중 하나를 사용하여 활동 로그를 보관하려면 구독에 대해 **로그 프로필** 을 설정합니다. 로그 프로필은 저장 또는 스트리밍되는 이벤트 및 출력(저장소 계정 및/또는 이벤트 허브)의 형식을 정의합니다. 또한 저장소 계정에 저장되는 이벤트에 대한 보존 정책(보존할 일 수)을 정의합니다. 보존 정책이 0으로 설정된 경우 이벤트 무기한으로 저장됩니다. 그렇지 않으면 1에서 365 사이의 값으로 설정할 수 있습니다. 보존 정책은 매일 적용되므로 하루의 마지막에(UTC) 보존 정책이 지난 날의 로그가 삭제됩니다. 예를 들어, 하루의 보존 정책이 있는 경우 오늘 날짜가 시작될 때 하루 전의 로그가 삭제됩니다. 삭제 프로세스는 자정(UTC)에 시작되지만, 저장소 계정에서 로그가 삭제될 때까지 최대 24시간이 걸릴 수 있습니다. [여기에서 로그 프로필에 대한 자세한 내용을 확인할 수 있습니다](../../azure-monitor/platform/activity-logs-overview.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-the-activity-log-using-the-portal"></a>포털을 사용하여 활동 로그 보관
1. 포털의 왼쪽 탐색에서 **활동 로그** 링크를 클릭합니다. 활동 로그에 대한 링크가 보이지 않으면 **모든 서비스** 링크를 먼저 클릭합니다.
   
    ![활동 로그 블레이드로 이동](media/archive-activity-log/activity-logs-portal-navigate-v2.png)
2. 블레이드 맨 위에서 **이벤트 허브로 내보내기**를 클릭합니다.
   
    ![내보내기 단추 클릭](media/archive-activity-log/activity-logs-portal-export-v2.png)
3. 표시되는 블레이드에서 **저장소 계정에 내보내기** 에 대한 상자를 선택하고 저장소 계정을 선택합니다.
   
    ![저장소 계정 설정](media/archive-activity-log/act-log-portal-export-blade.png)
4. 슬라이더 또는 텍스트 상자를 사용하여 저장소 계정에 활동 로그 이벤트를 보관해야 할 일 수(0~365)를 정의합니다. 데이터를 저장소 계정에 무기한으로 유지하려는 경우 이 숫자를 0으로 설정합니다. 365보다 많은 일 수를 입력해야 하는 경우 아래에 설명된 PowerShell 또는 CLI 메서드를 사용합니다.
5. **저장**을 클릭합니다.

## <a name="archive-the-activity-log-via-powershell"></a>PowerShell을 통해 활동 로그 보관

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

   ```powershell
   # Settings needed for the new log profile
   $logProfileName = "default"
   $locations = (Get-AzLocation).Location
   $locations += "global"
   $subscriptionId = "<your Azure subscription Id>"
   $resourceGroupName = "<resource group name your storage account belongs to>"
   $storageAccountName = "<your storage account name>"

   # Build the storage account Id from the settings above
   $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

   Add-AzLogProfile -Name $logProfileName -Location $locations -StorageAccountId $storageAccountId
   ```

| 자산 | 필수 | 설명 |
| --- | --- | --- |
| StorageAccountId |예 |활동 로그를 저장할 Storage 계정의 리소스 ID입니다. |
| 위치 |예 |활동 로그 이벤트를 수집할 쉼표로 구분된 지역 목록입니다. `(Get-AzLocation).Location`을 사용하여 구독에 대한 모든 지역 목록을 볼 수 있습니다. |
| RetentionInDays |아닙니다. |이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다. 0 값은 로그를 무기한(영원히) 저장합니다. |
| 범주 |아닙니다. |수집할 쉼표로 구분된 이벤트 범주 목록입니다. 가능한 값은 쓰기, 삭제 및 작업입니다.  지정하지 않으면 가능한 모든 값을 가정합니다. |

## <a name="archive-the-activity-log-via-cli"></a>CLI를 통해 활동 로그 보관

   ```azurecli-interactive
   az monitor log-profiles create --name "default" --location null --locations "global" "eastus" "westus" --categories "Delete" "Write" "Action"  --enabled false --days 0 --storage-account-id "/subscriptions/<YOUR SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP NAME>/providers/Microsoft.Storage/storageAccounts/<STORAGE ACCOUNT NAME>"
   ```

| 자산 | 필수 | 설명 |
| --- | --- | --- |
| 이름 |예 |로그 프로필의 이름입니다. |
| storage-account-id |예 |활동 로그를 저장할 Storage 계정의 리소스 ID입니다. |
| 위치 |예 |활동 로그 이벤트를 수집할 공백으로 구분된 지역 목록입니다. `az account list-locations --query [].name`을 사용하여 구독에 대한 모든 지역 목록을 볼 수 있습니다. |
| days |예 |이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다. 0 값은 로그를 무기한(영원히) 저장합니다.  0이면 활성화된 매개 변수를 true로 설정해야 합니다. |
|사용 | 예 |True 또는 False입니다.  보존 정책을 사용하거나 비활성화하는 데 사용합니다.  True이면 일 매개 변수 0보다 큰 값이어야 합니다.
| 범주 |예 |수집해야 할 공백으로 구분된 이벤트 범주 목록입니다. 가능한 값은 쓰기, 삭제 및 작업입니다. |

## <a name="storage-schema-of-the-activity-log"></a>활동 로그의 저장소 스키마
보관을 설정한 후 활동 로그 이벤트가 발생하는 즉시 저장소 계정에 저장소 컨테이너가 만들어집니다. 컨테이너 내의 Blob은 다음과 같이 설명된 활동 로그 및 진단 로그에 대해 동일한 명명 규칙을 따릅니다.

```
insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

예를 들어 Blob 이름은 다음과 같습니다.

```
insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

각 PT1H.json Blob은 Blob URL에 지정된 시간 내에서 발생한 이벤트의 JSON Blob을 포함합니다(예: h=12). 현재 시간 동안 이벤트는 발생하는 순서대로 PT1H.json 파일에 추가됩니다. 활동 로그 이벤트는 시간당 개별 Blob으로 나뉘므로 분 값(m=00)은 항상 00입니다.

PT1H.json 파일 내에서 각 이벤트는 이 형식에 따라 "레코드" 배열에 저장됩니다.

``` JSON
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| 요소 이름 | 설명 |
| --- | --- |
| 실시간 |이벤트에 해당하는 요청을 처리한 Azure 서비스에 의해 이벤트가 생성된 타임스탬프입니다. |
| ResourceId |영향을 받는 리소스의 리소스 ID입니다. |
| operationName |작업의 이름입니다. |
| 카테고리 |작업의 범주 (예: 쓰기, 읽기, 작업) |
| resultType |결과의 형식 (예: 성공, 실패, 시작) |
| resultSignature |리소스 종류에 따라 다릅니다. |
| durationMS |밀리초 단위의 작업 기간 |
| callerIpAddress |가용성을 기반으로 작업, UPN 클레임 또는 SPN 클레임을 수행한 사용자의 IP 주소입니다. |
| CorrelationId |일반적으로 문자열 형식의 GUID입니다. 동일한 uber 작업에 속하는 correlationId를 공유하는 이벤트입니다. |
| ID |권한 부여 및 클레임을 설명하는 JSON Blob입니다. |
| 권한 부여 |이벤트의 RBAC 속성 Blob입니다. 일반적으로 "action", "role" 및 "scope" 속성이 포함됩니다. |
| level |이벤트의 수준입니다. 해당 값은 “Critical”, “Error”, “Warning”, “Informational” 및 “Verbose” 중 하나입니다. |
| location |발생하는 위치의 지역(또는 전역)입니다. |
| properties |이벤트에 대한 세부 정보를 설명하는 `<Key, Value>` 쌍의 집합(즉, 사전)입니다. |

> [!NOTE]
> 해당 속성의 속성 및 사용은 리소스에 따라 달라질 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [분석을 위한 Blob 다운로드](../../storage/blobs/storage-quickstart-blobs-dotnet.md)
* [활동 로그를 Event Hubs로 스트리밍](../../azure-monitor/platform/activity-logs-stream-event-hubs.md)
* [활동 로그에 대한 자세한 내용](../../azure-monitor/platform/activity-logs-overview.md)



---
title: 가격 책정 및 대금 청구 - Azure Logic Apps | Microsoft Docs
description: Azure Logic Apps의 가격 책정 및 대금 청구 방식 알아보기
services: logic-apps
ms.service: logic-apps
ms.suite: logic-apps
author: kevinlam1
ms.author: klam
ms.reviewer: estfan, LADocs
manager: carmonm
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.topic: article
ms.date: 02/26/2019
ms.openlocfilehash: 9b5452f112c6325dafd5edbe693b90ec2a94abc0
ms.sourcegitcommit: f7f4b83996640d6fa35aea889dbf9073ba4422f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2019
ms.locfileid: "56990240"
---
# <a name="pricing-model-for-azure-logic-apps"></a>Azure Logic Apps용 가격 책정 모델

Azure Logic Apps를 사용하는 경우 클라우드에서 확장할 수 있는 자동화된 통합 워크플로를 만들고 실행할 수 있습니다. 다음은 Logic Apps의 청구 및 가격 책정 방식에 대한 세부 정보입니다. 

<a name="consumption-pricing"></a>

## <a name="consumption-pricing-model"></a>소비 가격 책정 모델

공용 또는 “글로벌” Logic Apps 서비스에서 실행되는 새 논리 앱의 경우에는 사용량만큼만 요금을 지불하면 됩니다. 이러한 논리 앱은 사용량 기반 계획 및 가격 책정 모델을 사용합니다. 논리 앱 정의에서 각 단계는 작업입니다. 작업은 트리거, 제어 흐름 단계, 기본 제공 작업 및 커넥터 호출을 포함합니다. Logic Apps는 논리 앱에서 실행되는 모든 작업을 측정합니다.  
자세한 내용은 [Logic Apps 가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)을 참조하세요.

<a name="fixed-pricing"></a>

## <a name="fixed-pricing-model"></a>고정 가격 책정 모델

내에서 실행 되는 새 논리 앱에 대 한는 [ *통합 서비스 환경* (ISE)](../logic-apps/connect-virtual-network-vnet-isolated-environment-overview.md), 기본 제공 작업 및 표준 커넥터에 대 한 고정된 된 월간 가격을 지불 합니다. ISE는 Azure 가상 네트워크의 리소스에 액세스할 수 있는 격리된 논리 앱을 만들고 실행하는 방법을 제공합니다. 

ISE 기본 단위 용량을 가지 며 고정에 더 많은 처리량을 할 경우 수 있도록 [배율 단위를 더 추가](../logic-apps/connect-virtual-network-vnet-isolated-environment.md#add-capacity), 생성 중 전이나 합니다. ISE는 원하는 만큼 많은 연결을 포함하는 하나의 체험 엔터프라이즈 커넥터를 포함합니다. 추가 엔터프라이즈 커넥터에 대한 사용량은 기업 소비량 금액을 기준으로 요금이 청구됩니다. 

> [!NOTE]
> ISE에는 [ *공개 미리 보기*](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)합니다. 자세한 내용은 [Logic Apps 가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)을 참조하세요.

<a name="triggers"></a>

## <a name="triggers"></a>트리거

트리거는 특정 이벤트가 발생할 때 논리 앱 인스턴스를 만드는 특수 작업입니다. 트리거는 논리 앱이 계량되는 방식에 영향을 주는 다양한 방법으로 작동합니다.

* **폴링 트리거** – 이 트리거는 논리 앱 인스턴스를 만들고 워크플로를 시작하는 조건을 충족하는 메시지에 대한 엔드포인트를 지속적으로 확인합니다. 논리 앱 인스턴스를 만들지 않은 경우에도 Logic Apps는 각 폴링 요청을 실행으로 측정합니다. 폴링 간격을 설정하려면 논리 앱 디자이너를 통해 트리거를 설정합니다.

  [!INCLUDE [logic-apps-polling-trigger-non-standard-metering](../../includes/logic-apps-polling-trigger-non-standard-metering.md)]

* **웹후크 트리거** – 이 트리거는 클라이언트가 특정 엔드포인트에 요청을 보낼 때까지 대기합니다. 웹후크 엔드포인트로 전송된 각 요청은 작업 실행으로 계산됩니다. 예를 들어, 요청 및 HTTP 웹후크 트리거는 둘 다 웹후크 트리거입니다.

* **되풀이 트리거** – 이 트리거는 트리거에 구성한 되풀이 간격을 기반으로 논리 앱 인스턴스를 만듭니다. 예를 들어 3일마다 또는 더 복잡한 일정으로 실행되는 되풀이 트리거를 설정할 수 있습니다.

## <a name="actions"></a>작업

Logic Apps는 원시 작업으로 기본 제공 작업을 측정합니다. 예를 들어 기본 제공 작업은 HTTP를 통한 호출, Azure Functions 또는 API Management의 호출 및 루프 및 조건과 같은 제어 흐름 단계를 포함합니다. 
- 각각 자신의 작업 유형이 있습니다. [커넥터](https://docs.microsoft.com/connectors)를 호출하는 작업에는 "ApiConnection" 유형이 있습니다. 이러한 커넥터는 표준 또는 엔터프라이즈 커넥터로 분류되며 해당 [가격 책정][pricing]을 기준으로 계량됩니다. 엔터프라이즈 커넥터 *미리 보기*는 표준 커넥터 요금이 청구됩니다.

Logic Apps는 성공 및 실패한 모든 실행 작업을 작업 실행으로 측정합니다. Logic Apps는 이러한 작업을 측정하지 않습니다. 

* 충족되지 않은 조건으로 인해 건너뛰는 작업
* 완료하기 전에 논리 앱이 중지되어 실행되지 않는 작업

비활성화된 논리 앱은 새 인스턴스를 만들 수 없으므로 비활성화된 동안 요금이 청구되지 않습니다.

> [!NOTE]
> 논리 앱을 사용 중지하면 현재 실행 중인 인스턴스가 완전히 중지되기까지 조금 시간이 걸릴 수 있습니다.

루프 내에서 실행되는 작업의 경우 Logic Apps는 루프의 주기별로 각 작업을 계산합니다. 예를 들어 목록을 처리하는 "for each" 루프가 있다고 가정합니다. Logic Apps는 목록 항목의 수를 루프의 작업 수와 곱하여 해당 루프에서 작업을 측정하고, 루프를 시작하는 작업을 추가합니다. 10개 항목 목록에 대한 계산은 (10 * 1) + 1이므로 작업 실행은 11개가 됩니다.

## <a name="integration-account-usage"></a>통합 계정 사용량

소비 기반 사용량에는 추가 비용 없이 Logic Apps의 [B2B/EDI](logic-apps-enterprise-integration-b2b.md) 및 [XML 처리](logic-apps-enterprise-integration-xml.md) 기능을 탐색, 개발 및 테스트할 수 있는 [통합 계정](logic-apps-enterprise-integration-create-integration-account.md)에 적용됩니다. 지역당 하나의 통합 계정을 가질 수 있습니다. 각 통합 계정은 거래 업체, 규약, 맵, 스키마, 어셈블리, 인증서, 일괄 처리 구성 등을 포함하는 특정 [아티팩트 수](../logic-apps/logic-apps-limits-and-config.md)까지 저장할 수 있습니다.

또한 Logic Apps에는 지원되는 Logic Apps SLA와 함께 기본 및 표준 통합 계정이 제공됩니다. 메시지 처리만을 원하는 경우 또는 대규모 비즈니스 엔터티와 거래 파트너 관계가 있는 소규모 비즈니스 파트너 역할을 수행하려는 경우에는 기본 통합 계정을 사용할 수 있습니다. 표준 통합 계정은 더 복잡한 B2B 관계를 지원하며 관리할 수 있는 엔터티의 수를 늘립니다. 자세한 내용은 [Azure 가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)을 참조하세요.

## <a name="next-steps"></a>다음 단계

* [Logic Apps에 대한 자세한 정보][whatis]
* [첫 번째 논리 앱 만들기][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-overview.md
[create]: quickstart-create-first-logic-app-workflow.md


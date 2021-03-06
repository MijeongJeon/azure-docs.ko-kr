---
title: Azure Active Directory Identity Protection에서 활성 위험 이벤트를 닫는 방법 | Microsoft Docs
description: 활성 위험 이벤트를 닫는 옵션에 대해 알아봅니다.
services: active-directory
keywords: Azure Active Directory ID 보호, 클라우드 앱 검색, 애플리케이션 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책
documentationcenter: ''
author: MarkusVi
manager: daveba
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.subservice: identity-protection
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/24/2018
ms.author: markvi
ms.reviewer: raluthra
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50448cc5d4fe6714aa0cd29216209506eccf7a7c
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56201621"
---
# <a name="how-to-close-active-risk-events"></a>방법: 활성 위험 이벤트 닫기

[위험 이벤트](../reports-monitoring/concept-risk-events.md)에서 Azure Active Directory는 잠재적으로 손상된 사용자 계정에 대한 표시기를 감지합니다. 관리자는 모든 위험 이벤트를 닫아서 영향을 받는 사용자가 더 이상 위험에 처하지 않도록 하고 싶습니다.

이 문서에서는 활성 위험 이벤트를 닫아야 하는 추가 옵션에 대해 간략히 설명합니다.

## <a name="options-to-close-risk-events"></a>위험 이벤트를 닫는 옵션 

위험 이벤트의 상태는 **활성** 또는 **종료됨**입니다. 모든 활성 위험 이벤트는 사용자 위험 수준이라고 하는 값의 계산에 영향을 줍니다. 사용자 위험 수준은 계정이 손상된 가능성에 대한 표시기(낮음, 보통, 높음)입니다. 

활성 위험 이벤트를 닫기 위한 다음 옵션이 있습니다.

- 사용자 위험 정책이 있는 암호 재설정 필요

- 수동 암호 다시 설정
 
- 모든 위험 이벤트 해체 

- 수동으로 개별 위험 이벤트 닫기



## <a name="require-password-reset-with-a-user-risk-policy"></a>사용자 위험 정책이 있는 암호 재설정 필요

[사용자 위험 조건부 액세스 정책](howto-user-risk-policy.md)을 구성하면 지정된 사용자 위험 수준이 자동으로 감지된 경우 암호 변경을 요구할 수 있습니다. 

![암호 재설정](./media/howto-close-active-risk-events/13.png)

암호 재설정은 관련된 사용자의 모든 활성 위험 이벤트를 닫고 ID를 안전한 상태로 다시 전환합니다. 사용자 위험 정책은 자동화되어 있으므로 활성 위험 이벤트를 닫기 위해 선호되는 방법입니다. 영향을 받은 사용자와 지원 센터 또는 관리자 간에 상호 작용이 필요하지 않습니다.

그러나 사용자 위험 정책을 사용하는 것이 항상 적용 가능한 것은 아닙니다. 예를 들어 다음에 적용됩니다.

- 사용자가 MFA(Multi-Factor Authentication)에 등록되어 있지 않은 경우
- 활성 위험 이벤트가 있는 사용자가 삭제된 경우
- 조사 결과, 보고된 위험 이벤트가 합법적인 사용자에 의해 수행된 것으로 드러난 경우


## <a name="manual-password-reset"></a>수동 암호 다시 설정

사용자 위험 정책을 사용하여 암호 재설정을 요구하는 것이 불가능한 경우 수동 암호 재설정으로 닫힌 사용자의 모든 위험 이벤트를 가져올 수 있습니다.

![암호 재설정](./media/howto-close-active-risk-events/04.png)


관련 대화 상자에 암호를 다시 설정할 수 있는 두 가지 방법이 제공됩니다.

![암호 재설정](./media/howto-close-active-risk-events/05.png)


**임시 암호 생성** - 임시 암호를 생성하여 ID를 안전한 상태로 즉시 전환할 수 있습니다. 이 방법은 임시 암호가 무엇인지 알아야 하므로 영향을 받는 사용자와 상호 작용해야 합니다. 예를 들어 사용자에 대한 대체 이메일 주소 또는 사용자의 관리자에게 새 임시 암호를 보낼 수 있습니다. 암호가 임시적이기 때문에 사용자는 다음 로그인 중에 암호를 변경하라는 메시지를 받습니다.


**사용자가 암호를 재설정해야 함** - 사용자가 암호를 재설정하도록 요구하면 지원 센터 또는 관리자에게 문의하지 않고도 셀프 복구가 가능합니다. 사용자 위험 정책의 경우와 마찬가지로 이 방법은 MFA에 등록된 사용자에게만 적용됩니다. 아직 MFA에 등록되지 않은 사용자의 경우 이 옵션을 사용할 수 없습니다.


## <a name="dismiss-all-risk-events"></a>모든 위험 이벤트 해체

암호 재설정이 불가능한 경우 모든 위험 이벤트를 해제할 수도 있습니다. 

![암호 재설정](./media/howto-close-active-risk-events/03.png)

**모든 이벤트 해제**를 클릭하면 모든 이벤트가 닫히고 영향을 받는 사용자가 더 이상 위험에 노출되지 않습니다. 그러나 이 방법은 기존 암호에 영향을 주지 않으므로 관련된 ID를 안전한 상태로 다시 전환하지 않습니다. 이 방법에 대한 기본 설정된 사용 사례는 활성 위험 이벤트가 있는 삭제된 사용자입니다. 


## <a name="close-individual-risk-events-manually"></a>수동으로 개별 위험 이벤트 닫기

수동으로 개별 위험 이벤트를 닫을 수 있습니다. 수동으로 위험 이벤트를 닫아 사용자 위험 수준을 낮출 수 있습니다. 일반적으로 위험 이벤트는 관련된 조사에 대한 응답에서 수동으로 닫힙니다. 예를 들어, 사용자와 대화하면 활성 위험 이벤트가 더 이상 필요하지 않는 것으로 나타납니다. 
 
수동으로 위험 이벤트를 닫을 경우 다음 작업을 수행하여 위험 이벤트의 상태를 변경하도록 선택할 수 있습니다.

![작업](./media/howto-close-active-risk-events/06.png)

- **해결** - 위험 이벤트를 검사한 후에 ID 보호 외부에서 적절한 수정 작업을 수행하고 위험 이벤트가 닫힌 것으로 간주되어야 한다고 판단하는 경우 이벤트를 "해결됨"으로 표시합니다. 해결된 이벤트는 위험 이벤트의 상태를 닫힘으로 설정하고 위험 이벤트는 더 이상 사용자 위험에 영향을 주지 않습니다.

- **가양성으로 표시** - 경우에 따라 위험 이벤트를 조사하여 플래그 지정이 위험으로 잘못 지정되었음을 발견할 수 있습니다. 위험 이벤트를 가양성으로 표시하여 이러한 발생 횟수를 줄일 수 있습니다. 기계 학습 알고리즘이 나중에 비슷한 이벤트를 분류하는 작업을 개선하도록 합니다. 가양성 이벤트가 [닫힘] 상태이면 더 이상 사용자 위험에 영향을 주지 않습니다.

- **무시** - 수정 작업을 수행하지 않지만 위험 이벤트를 활성 목록에서 제거하려면 위험 이벤트를 무시로 표시할 수 있고 이벤트 상태가 닫히게 됩니다. 무시된 이벤트는 사용자 위험에 영향을 주지 않습니다. 이 옵션은 이례적인 상황에서만 사용해야 합니다.

- **다시 활성화** - 수동으로 종료된([해결], [가양성] 또는 [무시] 선택) 위험 이벤트는 이벤트 상태를 [활성]으로 설정하여 다시 활성화될 수 있습니다. 다시 활성화된 위험 이벤트는 사용자 위험 수준 계산에 영향을 줍니다. 수정(예: 보안 암호를 다시 설정)을 통해 닫힌 위험 이벤트를 다시 활성화할 수 없습니다.
  

## <a name="next-steps"></a>다음 단계

Azure AD ID 보호의 개요는 [Azure AD ID 보호 개요](overview.md)를 참조하세요.

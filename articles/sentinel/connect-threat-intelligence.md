---
title: Azure Sentinel 미리 보기에서 위협 인텔리전스 데이터 수집 | Microsoft Docs
description: Azure Sentinel를 위협 인텔리전스 데이터를 연결 하는 방법에 알아봅니다.
documentationcenter: na
author: rkarlin
manager: barbkess
editor: ''
ms.assetid: 56412543-5664-44c1-b026-2dbaf78a9a50
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 2/28/2019
ms.author: rkarlin
ms.openlocfilehash: 2c5a7dc08886e21ef8e287540d9139ec555b11a2
ms.sourcegitcommit: ad019f9b57c7f99652ee665b25b8fef5cd54054d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57242295"
---
# <a name="collect-data-from-threat-intelligence-providers"></a>위협 인텔리전스 공급자에서 데이터를 수집 합니다. 

> [!IMPORTANT]
> Azure Sentinel 현재 공개 미리 보기 중입니다.
> 이 미리 보기 버전은 서비스 수준 계약 없이 제공되며 프로덕션 워크로드에는 사용하지 않는 것이 좋습니다. 특정 기능이 지원되지 않거나 기능이 제한될 수 있습니다. 자세한 내용은 [Microsoft Azure Preview에 대한 추가 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.

Azure Sentinel에 데이터를 스트리밍하려면 후 보강할 수 해당 위협 인텔리전스 피드를 사용 하 여 조직 전체에서 사용 하는 합니다. 

교차 확인 하 고 경고 규칙 예를 들어, 특정 IP 주소에서 경고가 발생 하는 경우 true 위협 인텔리전스를 사용 하 여 수 있도록 위협 인텔리전스 공급자 통합 하는 경우 해당 IP 주소 최근에 발견 될 때 악성 여부를 알려 주는 수 있게 됩니다. 을 azure Sentinel와 통합할 수 있습니다 [위협 인텔리전스 공급자](https://aka.ms/graphsecuritytips)합니다. 

한 번의 클릭을 사용 하 여 Azure Sentinel에 위협 인텔리전스 공급자에서 로그를 스트리밍할 수 있습니다. 이 연결을 사용 하면 다양 한 유형의 IP 주소, 도메인, URL 등 관찰 가능 개체를 포함 하는 표시기를 통합할 수 있습니다 하 고 검색 하 고 사용자 지정 만들기에 대 한 파일 해시 규칙 Azure Sentinel를 경고 합니다.  

## <a name="prerequisites"></a>필수 조건  

- 전역 관리자 또는 보안 관리자 권한이 있는 사용자 

- Microsoft Intelligent Security Graph를 사용 하 여 위협 인텔리전스 응용 프로그램 통합 

## <a name="connect-to-threat-intelligence"></a>위협 인텔리전스에 연결 

1. 위협 인텔리전스 공급자를 이미 사용 중인 경우에 팁 응용 프로그램을 찾아 지표를 Microsoft에 전송할 Azure Sentinel으로 서비스를 지정 하는 권한을 부여 해야 합니다.  

2. Azure Sentinel 선택 **데이터 컬렉션** 클릭 하 고는 **위협 인텔리전스** 바둑판식으로 배열 합니다.

3. **Connect**를 클릭합니다. 

4. Log Analytics에서 관련 스키마를 사용 하 여 위협 인텔리전스 피드를 검색할 **ThreatIntelligenceIndicator**합니다. 

 
## <a name="next-steps"></a>다음 단계

이 문서에서는 Azure Sentinel 위협 인텔리전스 공급자에 연결 하는 방법을 알아보았습니다. Azure에서 감시 하는 방법에 대 한 자세한 내용은 다음 문서를 참조 합니다.

- Azure Sentinel 사용을 시작 하려면 Microsoft Azure를 구독을 해야 합니다. 구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.
- 에 대해 알아봅니다 하는 방법 [온 보 딩 데이터를 Azure Sentinel](quickstart-onboard.md), 및 [데이터에 잠재적 위협을 파악](quickstart-get-visibility.md)합니다.

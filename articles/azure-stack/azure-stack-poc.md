---
title: Azure Stack이란? | Microsoft Docs
description: Azure Stack을 사용하면 데이터 센터에서 Azure 서비스를 실행할 수 있습니다.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 02/25/2019
ms.author: jeffgilb
ms.reviewer: unknown
ms.custom: mvc
ms.lastreviewed: 02/25/2019
ms.openlocfilehash: 65894ccd9514bce1d429b336f8bd5e6674048e65
ms.sourcegitcommit: 1516779f1baffaedcd24c674ccddd3e95de844de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56820266"
---
# <a name="what-is-azure-stack"></a>Azure Stack이란?

Microsoft Azure Stack은 데이터 센터에서 Azure 서비스를 제공할 수 있는 하이브리드 클라우드 플랫폼입니다. 이 플랫폼은 개발 중인 비즈니스 요구 사항을 지원하도록 설계 되었습니다. Azure Stack은 에지와 연결이 끊어진 환경 등의 최신 응용 프로그램에 대한 새로운 시나리오를 사용하도록 설정하거나 특정 보안 및 규정 준수 요구 사항을 충족할 수 있습니다.

Azure Stack 두 가지 배포 옵션 사용자의 요구를 충족하기 위해 제공됩니다.


## <a name="azure-stack-development-kit"></a>Azure Stack 개발 키트

Microsoft [ASDK(Azure Stack Development Kit)](./asdk/asdk-what-is.md)는 Azure Stack에 대한 평가 및 학습에 사용할 수 있는 Azure Stack의 단일 노드 배포입니다.  도구 및 Api를 사용 하 여 앱을 빌드하는 개발자 환경으로 Azure를 사용 하 여 일치 하는 ASDK도 사용할 수 있습니다.

>[!Note]
>ASDK는 프로덕션 환경으로 사용되지 않습니다.

ASDK에는 다음과 같은 제한 사항이 있습니다.

* ASDK를 단일 Azure Active Directory (Azure AD) 또는 Active Directory Federation Services (AD FS) id 공급자와 연결 됩니다. 이 디렉터리에 여러 사용자를 만들고 각 사용자에게 구독을 할당할 수 있습니다.
* 없기 때문에 Azure Stack 구성 요소를 단일 호스트 컴퓨터에 배포 된, 제한 된 물리적 리소스 테 넌 트 리소스에 대해 사용할 수 있습니다. 이 구성은 규모와 성능 평가용 아닙니다.
* 네트워크 시나리오는 단일 호스트 및 NIC 배포 요구 사항으로 인해 제한됩니다.

## <a name="azure-stack-integrated-systems"></a>Azure Stack 통합 시스템
Azure Stack 통합 시스템은 Microsoft와 [하드웨어 파트너](https://azure.microsoft.com/overview/azure-stack/integrated-systems/)의 파트너십을 통해 제공되며, 클라우드 기반 혁신 및 컴퓨팅 관리 단순성을 제공하는 솔루션을 만듭니다. Azure Stack은 통합된 하드웨어 및 소프트웨어 시스템으로 제공되므로 클라우드에서 혁신할 수있는 기능과 함께 필요한 유연성과 제어 기능을 사용할 수 있습니다. Azure Stack 통합 시스템 4-16 노드에서 크기 및 하드웨어 파트너와 Microsoft에서 지원 됩니다.  Azure Stack 통합 시스템을 사용하여 새로운 시나리오를 만들고 프로덕션 워크로드에 맞는 새로운 솔루션을 배포합니다.

## <a name="next-steps"></a>다음 단계

[주요 기능 및 개념](azure-stack-key-features.md)

[Azure Stack: Azure (pdf)의 확장](https://azure.microsoft.com/resources/azure-stack-an-extension-of-azure/)

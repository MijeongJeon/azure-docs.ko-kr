---
title: 변화하는 요구를 수용하기 위해 Azure 데이터 탐색기 클러스터 크기 조정
description: 이 문서는 수직 확장 및 수요 변화에 따라 Azure 데이터 탐색기 클러스터를 축소 하는 단계를 설명 합니다.
author: radennis
ms.author: radennis
ms.reviewer: v-orspod
ms.service: data-explorer
services: data-explorer
ms.topic: conceptual
ms.date: 02/18/2019
ms.openlocfilehash: a74c529fc3543d5cbdcf009a5b7736309e15569e
ms.sourcegitcommit: fdd6a2927976f99137bb0fcd571975ff42b2cac0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56961706"
---
# <a name="manage-cluster-scale-up-to-accommodate-changing-demand"></a>변화하는 요구를 수용하도록 클러스터 확장 관리

클러스터 크기를 적절하게 조정하는 것은 Azure 데이터 탐색기의 성능에 중요합니다. 하지만 절대 정확도 사용 하 여 클러스터에 대 한 수요를 예측할 수 없습니다. 정적 클러스터 크기는 모두 적합 미달 사용 또는 초과 사용, 발생할 수 있습니다.

하는 것이 좋습니다 *확장* 클러스터를 추가 하 고 용량 및 요청을 변경 하 여 CPU 리소스를 제거 합니다. 크기 조정에 대 한 두 가지 워크플로가 있습니다: 스케일 업 및 스케일 아웃 합니다. 이 문서에서는 클러스터 규모를 관리 하는 방법을 보여 줍니다.

1. 클러스터로 이동 합니다. 아래 **설정을**를 선택 **강화**합니다.

    사용 가능한 Sku의 목록을 표시 하 고 있습니다. 예를 들어, 다음 그림에서는 4 개의 Sku 사용할 수 있습니다.

    ![강화](media/manage-cluster-scale-up/scale-up.png)

    Sku는 현재 SKU 이므로 또는 클러스터 위치한 지역에서 사용할 수 없습니다 때문에 비활성화 됩니다.

1. SKU를 변경 하려면을 선택 하는 SKU를 선택 합니다 **선택** 단추입니다.

> [!NOTE]
> 확장 프로세스는 몇 분 정도 걸릴 수 있습니다 하 고이 시간 동안 클러스터를 일시 중단 됩니다. 크기를 축소하면 클러스터 성능이 손상될 수 있습니다.

이제 데이터 탐색기 Azure 클러스터에 대 한 강화 또는 규모 축소 작업을 완료 했으면 합니다. 할 수도 있습니다 [클러스터 스케일 아웃 관리](manage-cluster-scale-out.md) 를 동적으로 인스턴스 수를 지정 하는 기준에 따라 규모를 확장 합니다.

클러스터 크기 조정 문제를 사용 하 여 도움이 필요 하면 [지원 요청을 여세요](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) Azure portal에서 합니다.

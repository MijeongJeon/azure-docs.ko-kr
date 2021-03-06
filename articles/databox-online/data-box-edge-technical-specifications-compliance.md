---
title: Microsoft Azure 데이터 가장자리가 상자의 기술 사양 및 규정 준수 | Microsoft Docs
description: 기술 사양 및 Azure 데이터 상자의 가장자리에 대 한 준수에 알아봅니다
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: article
ms.date: 03/12/2019
ms.author: alkohli
ms.openlocfilehash: 8ef35709e90c0a58cc0ff8df1afb6e864adc0a23
ms.sourcegitcommit: 4133f375862fdbdec07b70de047d70c66ac29d50
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2019
ms.locfileid: "57994713"
---
# <a name="azure-data-box-edge-technical-specifications-preview"></a>Azure 데이터 가장자리가 상자의 기술 사양 (미리 보기)

Microsoft Azure 데이터 상자 Edge 장치의 하드웨어 구성 요소 기술 사양 및이 문서에서 설명 하는 규제 표준을 준수 합니다. 전원 공급 장치 (PSUs), 저장소 용량, 엔클로저 및 환경 표준 기술 사양에 설명합니다. 

> [!IMPORTANT]
> Data Box Edge는 미리 보기로 있습니다. 이 솔루션을 주문하고 배포하기 전에 [미리 보기에 대한 Azure 서비스 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 검토하세요. 

## <a name="power-supply-unit-specifications"></a>전원 공급 장치 사양

데이터 상자 Edge 장치에 두 100 240 V 전원 공급 장치 (PSUs) 고성능 팬을 있습니다. 두 PSUs 중복 전원 구성을 제공합니다. PSU가 실패 하면 장치 계속 실패 한 모듈이 교체 될 때까지 다른 PSU에서 정상적으로 작동 합니다. 다음 표에서 PSUs의 기술적을 보여 줍니다.

| 사양           | 750 W PSU                  |
|-------------------------|----------------------------|
| 최대 출력 전원    |  750 W                     |
| Frequency(빈도)               | 50/60Hz                   |
| 전압 범위 선택 | 자동 범위 지정: 100-240 V AC |
| 핫 플러그형           | 예                        |

<!--## Power consumption statistics

The following table lists the typical power consumption data (actual values may vary from the published) for the Data Box Edge device.-->

## <a name="storage-specifications"></a>저장소 사양

데이터 가장자리가 상자의 장치에는 1.6TB 용량을 사용 하 여 각 10 X 2.5"NVMe Ssd에. 이러한 ssd 2 운영 체제 디스크가 및 다른 8 개의 데이터 디스크가 있습니다. 장치에 대 한 총 사용 가능한 용량은 약 12.5TB 인. 다음 테이블에 장치의 저장소 용량에 대 한 세부 정보입니다.

|     사양                          |     값             |
|--------------------------------------------|-----------------------|
|    SSD(반도체 드라이브)의 수     |    8                  |
|    단일 SSD 용량                     |    1.6TB             |
|    총 용량                          |    12.8 TB            |
|    총 사용 가능한 용량 *                  |    ~ 12.5TB            |

**일부 공간 내부 용도로 예약 되어 있습니다.*

## <a name="enclosure-dimensions-and-weight-specifications"></a>엔클로저 차원과 가중치 사양

다음 표에서 크기 및 무게에 대해 다양한 엔클로저 사양을 보여줍니다.

### <a name="enclosure-dimensions"></a>엔클로저 크기

다음 표에서 인치 및 밀리미터로 엔클로저의 크기를 나타냅니다.

|     인클로저     |     밀리미터     |     인치     |
|-------------------|---------------------|----------------|
|    높이         |    304.8            |    12          |
|    너비          |    660.4            |    26          |
|    깊이          |    1041.4           |    41          |

### <a name="enclosure-weight"></a>엔클로저 무게

장치 패키지 66 lbs를 비교 합니다. 및 처리에 두 명이 필요 합니다. 장치의 무게 인클로저 구성에 따라 달라 집니다.

|     인클로저                                 |     무게          |
|-----------------------------------------------|---------------------|
|    패키지를 포함 하 여 총 가중치       |    66 lbs 합니다.          |
|    장치의 무게                       |    48.3 lbs 합니다.        |

## <a name="enclosure-environment-specifications"></a>엔클로저 환경 사양

이 섹션에 온도, 습도, 고도 등는 엔클로저 환경과 관련 된 사양을 나열 합니다.

### <a name="temperature-and-humidity"></a>온도 및 습도

|     인클로저         |     주변 온도 범위     |     주변 상대 습도     |     최대 이슬점     |
|-----------------------|--------------------------------------|--------------------------------------|---------------------------|
|    작동        |    10 ° C-35 ° C (50 ° F-86 ° F)         |    10% ~ 80% 비-압축 합니다.         |    29°C(84°F)            |
|    작동 불가능    |    -40 ° C 65 ° c (-40 ° F-149 ° F)     |    5% ~ 95% 비-압축 합니다.          |    33 ° C (91 ° F)            |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>기류, 고도, 충격, 진동, 방향, 안전성 및 EMC

|     인클로저                           |     운영 사양                                                                                                                                                                                         |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    기류                              |    시스템의 공기는 앞에서 뒤로 흐릅니다. 압력이 낮고, 후면 배기가 설치된 시스템을 작동할 수 있어야 합니다. <!--Back pressure created by rack doors and obstacles should not exceed 5 pascals (0.5 mm water gauge).-->    |
|    최대 높이 운영        |    최대 작동 등급 취소 온도 3048 미터 (10, 000 피트)에 따른 [작동 해제 사양 등급 온도](#operating-temperature-de-rating-specifications)합니다.                                                                                |
|    최대 고도, 작동 불가능    |    12,000 미터 (39,370 피트)                                                                                                                                                                                         |
|    충격, 작동                   |    11 밀리초 6 방향에 대 한 6 G                                                                                                                                                                         |
|    충격, 작동 불가능               |    6 방향에서 2 시간 (밀리초)에 대 한 71 G                                                                                                                                                                           |
|    진동, 작동               |    로 0.26 G<sub>RMS</sub> 임의 350 Hz 5 반면                                                                                                                                                                                     |
|    진동, 작동 불가능           |    1.88 G<sub>RMS</sub> 10 반면 500 Hz 15 분 동안 (6 개 면 모두 테스트 합니다.)                                                                                                                                                  |
|    방향 및 탑재             |    19"랙 탑재                                                                                                                                                                                        |
|    안전성 및 승인                 |    EN 60950-1:2006 +A1:2010 +A2:2013 +A11:2009 +A12:2011/IEC 60950-1:2005 ed2 +A1:2009 +A2:2013 EN 62311:2008                                                                                                                                                                       |
|    EMC                                  |    FCC A, ICES-003 <br>EN 55032:2012/CISPR 32:2012  <br>EN 55032:2015/CISPR 32:2015  <br>EN 55024:2010 +A1:2015/CISPR 24:2010 +A1:2015  <br>61000 EN-3-2:2014 / IEC 61000-3-2:2014 (클래스 D)   <br>EN 61000-3-3:2013/IEC 61000-3-3:2013                                                                                                                                                                                         |
|    에너지             |    아니요 (EU) 규정 수수료 617/2013                                                                                                                                                                                        |
|    RoHS           |    EN 50581:2012                                                                                                                                                                                        |


### <a name="operating-temperature-de-rating-specifications"></a>취소 사양 등급 운영 온도

|     온도 취소 등급 운영     |     주변 온도 범위                                                         |
|--------------------------------------------|------------------------------------------------------------------------------------------|
|    최대 35 ° C (95 ° F)                       |    최대 온도 여 ° 1c/300 m (1 ° F/547 ft) 950 m (3,117 ft) 위에 줄어듭니다.    |
|    35 ° C 40 ° c (104 ° f 95 ° F)            |    최대 온도 여 ° 1c/175 m (1 ° F/319 ft) 950 m (3,117 ft) 위에 줄어듭니다.    |
|    40 ° C 45 ° c (113 ° f 104 ° F)           |    최대 온도 여 ° 1c/125 m (1 ° F/228 ft) 950 m (3,117 ft) 위에 줄어듭니다.    |


## <a name="next-steps"></a>다음 단계

- [Azure Data Box Edge 배포](data-box-edge-deploy-prep.md)

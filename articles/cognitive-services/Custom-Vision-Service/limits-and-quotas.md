---
title: 가격 책정 및 한도 - Custom Vision Service
titlesuffix: Azure Cognitive Services
description: Custom Vision Service의 한도 및 할당량에 대해 알아봅니다.
services: cognitive-services
author: anrothMSFT
manager: nitinme
ms.service: cognitive-services
ms.subservice: custom-vision
ms.topic: conceptual
ms.date: 10/16/2018
ms.author: anroth
ms.openlocfilehash: 58109e17ed33e6af8dedf3ed8c1cc9ddf546a05e
ms.sourcegitcommit: 89b5e63945d0c325c1bf9e70ba3d9be6888da681
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57588672"
---
# <a name="pricing-and-limits"></a>가격 책정 및 제한

Custom Vision 서비스에 대해 3계층의 키가 있습니다. 제한된 평가판 프로젝트 리소스가 Custom Vision 로그인(즉, Azure Active Directory 계정 또는 MSA 계정)에 추가됩니다. 이러한 리소스는 서비스의 짧은 평가판에 사용되도록 제공됩니다. Azure Portal을 통해 F0(무료) 또는 S0(표준) 구독을 등록할 수 있습니다. 가격 책정 및 트랜잭션에 대한 자세한 내용은 해당 [Cognitive Services 가격 책정 페이지](https://azure.microsoft.com/pricing/details/cognitive-services/custom-vision-service/)를 참조하세요.

Azure 미리 보기(2018년 3월 1일) 도입 전에 초기 무료 미리 보기 동안 만들어진 계정의 경우 이전의 제한된 평가판용 할당량이 유지됩니다.

프로젝트당 학습 이미지 수 및 프로젝트당 태그 수는 S0 프로젝트에서 시간이 지남에 따라 증가될 것으로 예상됩니다.

||**제한된 평가판**|**F0**|**S0**|
|-----|-----|-----|-----|
|프로젝트|2|2|100|
|프로젝트당 학습 이미지, 분류|5,000|5,000|50,000|
|프로젝트당 학습 이미지, 개체 감지|5,000|5,000|10000|
|예측 수/월|10000 |10000|Unlimited|
|태그/프로젝트|50|50|250|
|반복 횟수 |10|10|10|
|태그당 레이블이 지정된 최소 이미지, 분류(50개 이상 권장) |5|5|5|
|태그당 레이블이 지정된 최소 이미지, 개체 검색(50개 이상 권장)|15|15|15|
|예측 이미지 저장 기간|30일|30일|30일|
|저장소가 있는 [예측](https://go.microsoft.com/fwlink/?linkid=865445) 작업(초당 트랜잭션 수)|2|2|10|
|저장소가 없는 [예측](https://go.microsoft.com/fwlink/?linkid=865445) 작업(초당 트랜잭션 수)|2|2|20|
|[TrainProject](https://go.microsoft.com/fwlink/?linkid=865446)(초당 API 호출 수)|2|2|10|
|[기타 API 호출](https://go.microsoft.com/fwlink/?linkid=865446)(초당 트랜잭션 수)|10|10|10|
|최대 이미지 크기(학습 이미지 업로드) |6MB|6MB|6MB|
|최대 이미지 크기(예측)|4MB|4MB|4MB|



---
title: 릴리스 정보 - Face API 서비스
titleSuffix: Azure Cognitive Services
description: Face API 서비스의 릴리스 정보에는 다양한 버전에 대한 릴리스 변경 기록이 포함됩니다.
services: cognitive-services
author: SteveMSFT
manager: nitinme
ms.service: cognitive-services
ms.subservice: face-api
ms.topic: conceptual
ms.date: 03/01/2018
ms.author: sbowles
ms.openlocfilehash: 1af699a4b28309e7b004ed1eedf339e142065e50
ms.sourcegitcommit: 90cec6cccf303ad4767a343ce00befba020a10f6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55878462"
---
# <a name="face-api-release-notes"></a>Face API 릴리스 정보

이 문서는 Face API 서비스 버전 1.0에 적용됩니다.

### <a name="release-changes-in-january-2019"></a>2019년 1월 릴리스 변경 내용

* 여러 구독 간 데이터 마이그레이션 기능을 지원하는 스냅숏 기능([스냅숏](https://docs.microsoft.com/rest/api/cognitiveservices/face/snapshot))이 추가되었습니다.

### <a name="release-changes-in-october-2018"></a>2018년 10월 릴리스 변경 내용

* [PersonGroup - 학습 상태 가져오기](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395247), [LargePersonGroup - 학습 상태 가져오기](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599ae32c6ac60f11b48b5aa5) 및 [LargeFaceList - 학습 상태 가져오기](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a1582f8d2de3616c086f2cf)에서 `status`, `createdDateTime`, `lastActionDateTime` 및 `lastSuccessfulTrainingDateTime`의 자세한 설명이 추가되었습니다.

### <a name="release-changes-in-may-2018"></a>2018년 5월 릴리스 변경 내용

* `age`, `glasses`, `facialHair`, `hair`, `makeup` 특성과 함께 `gender` 특성이 크게 향상되었습니다. [얼굴 - 검색](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) `returnFaceAttributes` 매개 변수를 통해 사용합니다. 

* [얼굴 - 검색](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), [FaceList - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250), [LargeFaceList - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a158c10d2de3616c086f2d3), [PersonGroup 사람 - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) 및 [LargePersonGroup 사람 - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adf2a3a7b9412a4d53f42)에서 입력 이미지 파일 크기 제한이 4MB에서 6MB로 증가했습니다.

### <a name="release-changes-in-march-2018"></a>2018년 3월 릴리스 변경 내용

* 사람/얼굴을 1백만 개까지 포함할 수 있는 대규모 컨테이너 [LargeFaceList](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a157b68d2de3616c086f2cc) 및 [LargePersonGroup](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acdee6ac60f11b48b5a9d)이 추가되었습니다. [대규모 기능을 사용하는 방법](Face-API-How-to-Topics/how-to-use-large-scale.md)의 자세한 내용입니다.

* [얼굴 - 식별](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) `maxNumOfCandidatesReturned` 매개 변수가 [1, 5]에서 [1, 100]으로 증가하고 기본값이 10으로 증가했습니다.

### <a name="release-changes-in-may-2017"></a>2017년 5월 릴리스 변경 내용

* [얼굴 - 검색](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) `returnFaceAttributes` 매개 변수에서 `hair`, `makeup`, `accessory`, `occlusion`, `blur`, `exposure` 및 `noise` 특성이 추가되었습니다.

* PersonGroup 및 [얼굴 - 식별](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)에서만 10K의 사람이 지원되었습니다.

* `start` 및 `top`이라는 선택적 매개 변수가 있는 [PersonGroup 사람 - 목록](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395241)에 페이지 매김이 지원되었습니다.

* 다른 FaceLists 및 PersonGroup의 다른 사람에 대해 얼굴이 추가/삭제되는 경우 동시성이 지원되었습니다.

### <a name="release-changes-in-march-2017"></a>2017년 3월 릴리스 변경 내용
* [얼굴 - 검색](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) `returnFaceAttributes` 매개 변수에서 `emotion` 특성이 추가되었습니다.

* 얼굴이 [FaceList - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250) 및 [PersonGroup 사람 - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b)의 `targetFace`인 [얼굴 - 검색](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236)에서 반환된 사각형을 사용하여 다시 검색될 수 없도록 수정했습니다.

* 36x36과 4096x4096 픽셀 간이 엄격하게 되도로 감지할 수 있는 글꼴 크기가 수정되었습니다.

### <a name="release-changes-in-november-2016"></a>2016년 11월 릴리스 변경 내용
* 식별이나 유사성 검사를 위해 [PersonGroup 사람 - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) 또는 [FaceList - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250)를 사용할 경우 추가로 유지될 얼굴을 저장하는 Face Storage 표준을 추가했습니다. 저장된 이미지는 1,000개 얼굴 기준으로 $0.5로 청구되며, 이 요금은 일별로 계산됩니다. 무료 계층 구독은 총 1,000명의 사람으로 계속 제한됩니다.

### <a name="release-changes-in-october-2016"></a>2016년 10월 릴리스 변경 내용
* [FaceList - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250) 및 [PersonGroup 사람 - 얼굴 추가](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b)에서 targetFace의 얼굴이 둘 이상인 오류 메시지를 '이미지에 둘 이상의 얼굴들이 있습니다.'에서 '이미지에 둘 이상의 얼굴이 있습니다.'로 변경했습니다.

### <a name="release-changes-in-july-2016"></a>2016년 7월 릴리스 변경 내용
* [얼굴 - 확인](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a)에서 사람 개체 인증에 얼굴이 지원되었습니다.

* 두 작업 모드의 선택 영역을 사용하도록 설정하는 선택적 `mode` 매개 변수가 추가되었습니다. [얼굴 - 유사 항목 찾기](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237)에서 `matchPerson` 및 `matchFace`이며 기본값은 `matchPerson`입니다.

* [얼굴 - 식별](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)에서 한 얼굴이 사람 개체에 속하는지 여부의 임계값을 설정하도록 사용자에 대한 선택 사항 `confidenceThreshold` 매개 변수를 추가했습니다.

* 사용자가 시작점 및 목록에 대한 총 PersonGroups 수를 지정할 수 있도록 [PersonGroup - 목록](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395248)에서 선택 사항 `start` 및 `top` 매개 변수를 추가했습니다.

### <a name="v10-changes-from-v0"></a>V0에서 변경된 V1.0 내용
* 서비스 루트 엔드포인트를 ```https://westus.api.cognitive.microsoft.com/face/v0/```에서 ```https://westus.api.cognitive.microsoft.com/face/v1.0/```으로 업데이트했습니다. 변경 내용 적용 대상은 [Face - 검색](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), [Face - 식별](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [Face - 유사 항목 찾기](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237) 및 [Face - 그룹](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238)입니다.

* 36x36픽셀로 감지 가능한 최소 얼굴 크기를 업데이트했습니다. 36x36픽셀보다 작은 얼굴은 검색되지 않습니다.

* Face V0에서 PersonGroup 및 사람 데이터가 사용되지 않았습니다. Face V1.0 서비스를 사용하여 해당 데이터에 액세스할 수 없습니다.

* 2016년 6월 30 일에 Face API의 V0 엔드포인트가 사용되지 않았습니다.

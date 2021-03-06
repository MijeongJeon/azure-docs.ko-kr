---
title: Text Analytics란?
titleSuffix: Azure Cognitive Services
description: 감성 분석, 핵심 구 추출, 언어 감지 및 엔터티 링크 설정에 대한 Azure Cognitive Services의 Text Analytics입니다.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: overview
ms.date: 02/13/2019
ms.author: aahi
ms.openlocfilehash: 7623f98b9fd6c4bad8a41050e39b6e0e8650dccc
ms.sourcegitcommit: 24906eb0a6621dfa470cb052a800c4d4fae02787
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56889289"
---
# <a name="what-is-text-analytics"></a>Text Analytics란?

텍스트 분석 API는 클라우드 기반 서비스로 원시 텍스트에 대한 고급 자연어 처리를 제공하며, 감성 분석, 핵심 구 추출, 언어 감지 및 엔터티 링크의 네 가지 주요 기능을 포함합니다.

이 API는 개발 프로젝트를 위한 클라우드의 기계 학습 및 AI 알고리즘 모음인 [Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/)의 일부입니다.

## <a name="capabilities-in-text-analytics"></a>Text Analytics의 기능

텍스트 분석은 다른 작업을 의미할 수 있지만, Cognitive Services의 Text Analytics API는 다음 표에 설명된 것처럼 네 가지 유형의 분석을 제공합니다.

| 작업| 설명 | API |
|-----------|-------------|------|
|[**감정 분석**](how-tos/text-analytics-how-to-sentiment-analysis.md) | 원시 텍스트에서 긍정적이거나 부정적인 감정의 단서를 분석하여 브랜드 또는 주제에 대한 고객의 생각을 알아봅니다. 이 API는 각 문서에 대해 0과 1 사이의 감점 점수를 반환합니다. 여기서 1이 가장 긍정적인 것입니다.<br /> 분석 모델은 Microsoft의 포괄적인 텍스트 본문 및 자연어 기술을 사용하여 미리 학습됩니다. 이 API는 [선택된 언어](text-analytics-supported-languages.md)에 대해 사용자가 제공하는 원시 텍스트를 분석하고 점수를 매겨 호출 애플리케이션에 직접 결과를 반환할 수 있습니다. | [REST (영문)](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9) <br /> [.NET](https://docs.microsoft.com/azure/cognitive-services/text-analytics/quickstarts/csharp#install-the-nuget-sdk-package)  |
|[**핵심 구 추출**](how-tos/text-analytics-how-to-keyword-extraction.md) | 자동으로 핵심 구를 추출하여 요점을 빠르게 파악합니다. 예를 들어 "The food was delicious and there were wonderful staff"라는 입력 텍스트에 대해 이 API는 "food" 및 "wonderful staff"이라는 핵심 발화 지점을 반환합니다.  | [REST (영문)](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) <br /> [.NET](https://docs.microsoft.com/azure/cognitive-services/text-analytics/quickstarts/csharp#install-the-nuget-sdk-package) |
|[**언어 감지**](how-tos/text-analytics-how-to-language-detection.md) | 최대 120개 언어에 대해, 입력 텍스트를 쓴 언어를 감지하고 요청에 따라 제출된 모든 문서에 대해 단일 언어 코드를 보고합니다. 언어 코드가 점수와 쌍을 이루어 점수의 강도를 나타냅니다. | [REST (영문)](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7) <br />  [.NET](https://docs.microsoft.com/azure/cognitive-services/text-analytics/quickstarts/csharp#install-the-nuget-sdk-package) |
|[**엔터티 인식(미리 보기)**](how-tos/text-analytics-how-to-entity-linking.md) | 텍스트의 엔터티를 인물, 장소, 조직, 날짜/시간, 수량, 백분율, 통화 등으로 식별하고 분류합니다. 잘 알려진 엔터티도 인식되고, 웹에서 더 많은 정보에 연결됩니다. | [REST (영문)](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics-V2-1-Preview/operations/5ac4251d5b4ccd1554da7634) |

## <a name="use-containers"></a>컨테이너 사용

[Text Analytics 컨테이너를 사용](how-tos/text-analytics-how-to-install-containers.md)하여 표준화된 Docker 컨테이너를 데이터와 가까이 설치함으로써 핵심 구를 추출하고, 언어를 검색하고, 로컬로 감정을 분석할 수 있습니다.

## <a name="typical-workflow"></a>일반적인 워크플로

간단한 워크플로: 분석을 위해 데이터를 제출하고 코드의 출력을 처리합니다. 분석기는 추가 구성 또는 사용자 지정 없이 있는 그대로 사용됩니다.

1. [액세스 키](how-tos/text-analytics-how-to-access-key.md)를 위해 [등록](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account)합니다. 이 키를 각 요청에 대해 전달해야 합니다.

2. 데이터를 구조화되지 않은 원시 텍스트로 포함하는 [요청을 JSON으로 구성](how-tos/text-analytics-how-to-call-api.md#json-schema)합니다.

3. 등록 동안 설정된 엔드포인트에 요청을 게시하고, 감정 분석, 핵심 구 추출, 언어 감지 또는 엔터티 ID 등, 원하는 리소스를 추가합니다.

4. 응답을 스트리밍하거나 로컬로 저장합니다. 요청에 따라, 결과는 감정 점수, 추출된 핵심 구 모음 또는 언어 코드가 됩니다.

출력은 ID를 기준으로 게시한 각 텍스트 문서에 대한 결과를 포함하는 단일 JSON 문서로 반환됩니다. 추후에 결과를 실행 가능한 정보로 분석하거나, 시각화하거나, 분류할 수 있습니다.

데이터는 계정에 저장되지 않습니다. Text Analytics API에서 수행하는 작업은 상태 비저장 작업입니다. 즉, 제공하는 텍스트가 처리된 후 결과가 즉시 반환됩니다.

<a name="supported-languages"></a>

## <a name="supported-languages"></a>지원되는 언어

이 섹션은 검색 가능성을 높이기 위해 별도 문서로 이동되었습니다. 이 콘텐츠에 대해서는 [Text Analytics API의 지원되는 언어](text-analytics-supported-languages.md)를 참조하세요.

<a name="data-limits"></a>

## <a name="data-limits"></a>데이터 제한

모든 Text Analytics API 엔드포인트는 원시 텍스트 데이터를 수락합니다. 현재 제한은 각 문서에 대해 5,120자입니다. 더 큰 문서를 분석해야 할 경우 더 작은 청크로 분리하면 됩니다. 여전히 더 높은 한도가 필요하면 [저희에게 문의](https://azure.microsoft.com/overview/sales-number/)하세요. 그러면 해결해 드릴 수 있습니다.

| 제한 | 값 |
|------------------------|---------------|
| 단일 문서의 최대 크기 | [`StringInfo.LengthInTextElements`](https://docs.microsoft.com/dotnet/api/system.globalization.stringinfo.lengthintextelements)로 측정해서 5,120자입니다. |
| 전체 요청의 최대 크기 | 1MB |
| 요청의 최대 문서 수 | 1,000개 문서 |

속도 제한은 분당 100개 호출입니다. 단일 호출에서 많은 수의 문서를 제출할 수 있습니다(최대 1,000개 문서).

## <a name="unicode-encoding"></a>유니코드 인코딩

Text Analytics API는 텍스트 표현 및 문자 수 계산에 유니코드 인코딩을 사용합니다. 측정 가능한 문자 수 차이 없이 UTF-8 및 UTF-16으로 요청을 제출할 수 있습니다. 유니코드 코드 포인트는 문자 길이에 대한 추론으로 사용되며, 텍스트 분석 데이터 제한을 위해 동일한 것으로 간주됩니다. [`StringInfo.LengthInTextElements`](https://docs.microsoft.com/dotnet/api/system.globalization.stringinfo.lengthintextelements)를 사용하여 문자 수를 확인하는 경우 데이터 크기 측정에 사용하는 것과 동일한 방법을 사용합니다.

## <a name="next-steps"></a>다음 단계

먼저 [대화형 데모](https://azure.microsoft.com/services/cognitive-services/text-analytics/)를 사용해봅니다. 텍스트 입력(최대 5,120자)을 붙여 넣어 언어를 감지(최대 120개)하거나, 감정 점수를 계산하거나, 핵심 구를 추출할 수 있습니다. 등록은 필요하지 않습니다.

API를 직접 호출할 준비가 되면 다음을 수행합니다.

+ 액세스 키를 얻기 위해 [등록](how-tos/text-analytics-how-to-signup.md)하고 [API 호출](how-tos/text-analytics-how-to-call-api.md) 단계를 검토합니다.

+ [빠른 시작](quickstarts/csharp.md)에서 C#으로 작성된 REST API를 연습할 수 있습니다. 최소의 코드로 텍스트를 제출하고, 분석을 선택하고, 결과를 보는 방법을 알아봅니다.

+ [API 참조 설명서](//go.microsoft.com/fwlink/?LinkID=759346)는 API에 대한 기술 설명서를 제공합니다. 이 설명서는 각 설명서 페이지에서 API를 호출할 수 있도록 포함된 호출을 지원합니다.

+ [외부 및 커뮤니티 콘텐츠](text-analytics-resource-external-community.md)는 다른 도구 및 기술과 함께 Text Analytics를 사용하는 방법을 보여 주는 블로그 게시물 및 비디오 목록을 제공합니다.

## <a name="see-also"></a>참고 항목

 [Cognitive Services 설명서 페이지](https://docs.microsoft.com/azure/cognitive-services/)

---
title: '빠른 시작: Python SDK'
titleSuffix: Azure Cognitive Services
description: 이 빠른 시작에서는 일반적인 작업에 Python SDK를 사용하는 방법을 알아봅니다.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: quickstart
ms.date: 02/26/2019
ms.author: pafarley
ms.openlocfilehash: d14b9c88b447583eedc8b50f4f9acf80ae4e3c75
ms.sourcegitcommit: 24906eb0a6621dfa470cb052a800c4d4fae02787
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56889633"
---
# <a name="azure-cognitive-services-computer-vision-sdk-for-python"></a>Python용 Azure Cognitive Services Computer Vision SDK

Computer Vision 서비스는 개발자에게 이미지를 처리하고 정보를 반환하는 고급 알고리즘에 대한 액세스를 제공합니다. Computer Vision 알고리즘은 관심 있는 시각적 기능에 따라 이미지의 콘텐츠를 다양한 방식으로 분석합니다. 

* [이미지 분석](#analyze-an-image)
* [주체 도메인 목록 가져오기](#get-subject-domain-list)
* [도메인 기준 이미지 분석](#analyze-an-image-by-domain)
* [이미지의 텍스트 설명 가져오기](#get-text-description-of-an-image)
* [이미지에서 필기한 텍스트 가져오기](#get-text-from-image)
* [썸네일 생성](#generate-thumbnail)

이 서비스에 대한 자세한 내용은 [Computer Vision이란?][computervision_docs]을 참조하세요.

자세한 설명서를 찾으시나요?

* [SDK 참조 설명서](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision)
* [Cognitive Services Computer Vision 설명서](https://docs.microsoft.com/azure/cognitive-services/computer-vision/)

## <a name="prerequisites"></a>필수 조건

* [Python 3.6+][python]
* 평가판 [Computer Vision 키][computervision_resource] 및 연결된 지역. 이러한 값은 [ComputerVisionAPI][ref_computervisionclient] 클라이언트 개체의 인스턴스를 만들 때 필요합니다. 이 값을 구하려면 다음 방법 중 하나를 사용합니다. 

### <a name="if-you-dont-have-an-azure-subscription"></a>Azure 구독이 없는 경우

**시도** 환경에서 7일 동안 유효한 평가판 키를 만듭니다. 키가 만들어지면 키와 지역 이름을 복사해 둡니다. 이 값은 [클라이언트를 만들 때](#create-client) 필요합니다.

키를 만든 후에는 다음을 유지합니다.

* 키 값: `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` 형식의 32자 문자열 
* 키 지역: 엔드포인트 URL인 https://**westcentralus**.api.cognitive.microsoft.com의 하위 도메인

### <a name="if-you-have-an-azure-subscription"></a>Azure 구독이 있는 경우

Computer Vision API 계정이 필요한 경우 구독에서 해당 계정을 만드는 가장 쉬운 방법은 다음 [Azure CLI][azure_cli] 명령을 사용하는 것입니다. 리소스 그룹 이름(예: "my-cogserv-group")을 선택하고 Computer Vision 리소스 이름(예: "my-computer-vision-resource")을 선택해야 합니다. 

```Bash
RES_REGION=westeurope 
RES_GROUP=<resourcegroup-name>
ACCT_NAME=<computervision-account-name>

az cognitiveservices account create \
    --resource-group $RES_GROUP \
    --name $ACCT_NAME \
    --location $RES_REGION \
    --kind ComputerVision \
    --sku S1 \
    --yes
```

<!--
## Installation

Install the Azure Cognitive Services Computer Vision SDK with [pip][pip], optionally within a [virtual environment][venv].

### Configure a virtual environment (optional)

Although not required, you can keep your base system and Azure SDK environments isolated from one another if you use a [virtual environment][virtualenv]. Execute the following commands to configure and then enter a virtual environment with [venv][venv], such as `cogsrv-vision-env`:

```Bash
python3 -m venv cogsrv-vision-env
source cogsrv-vision-env/bin/activate
```
-->

### <a name="install-the-sdk"></a>SDK 설치

[pip][pip]를 통해 Python용 Azure Cognitive Services Computer Vision SDK [패키지][pypi_computervision]를 설치합니다.

```Bash
pip install azure-cognitiveservices-vision-computervision
```

## <a name="authentication"></a>Authentication

Computer Vision 리소스를 만들면 클라이언트 개체를 인스턴스화하기 위해 해당 **지역** 및 해당 **계정 키** 중 하나가 필요합니다.

[ComputerVisionAPI][ref_computervisionclient] 클라이언트 개체의 인스턴스를 만들 때 이러한 값을 사용합니다. 

<!--

For example, use the Bash terminal to set the environment variables:

```Bash
ACCOUNT_REGION=<resourcegroup-name>
ACCT_NAME=<computervision-account-name>
```

### For Azure subscription usrs, get credentials for key and region

If you do not remember your region and key, you can use the following method to find them. If you need to create a key and region, you can use the method for [Azure subscription holders](#if-you-have-an-azure-subscription) or for [users without an Azure subscription](#if-you-dont-have-an-azure-subscription).

Use the [Azure CLI][cloud_shell] snippet below to populate two environment variables with the Computer Vision account **region** and one of its **keys** (you can also find these values in the [Azure portal][azure_portal]). The snippet is formatted for the Bash shell.

```Bash
RES_GROUP=<resourcegroup-name>
ACCT_NAME=<computervision-account-name>

export ACCOUNT_REGION=$(az cognitiveservices account show \
    --resource-group $RES_GROUP \
    --name $ACCT_NAME \
    --query location \
    --output tsv)

export ACCOUNT_KEY=$(az cognitiveservices account keys list \
    --resource-group $RES_GROUP \
    --name $ACCT_NAME \
    --query key1 \
    --output tsv)
```
-->

### <a name="create-client"></a>클라이언트 만들기

[ComputerVisionAPI][ref_computervisionclient] 클라이언트 개체를 만듭니다. 다음 코드 예제에서 지역과 키 값을 사용자의 값으로 변경합니다.

```Python
from azure.cognitiveservices.vision.computervision import ComputerVisionAPI
from azure.cognitiveservices.vision.computervision.models import VisualFeatureTypes
from msrest.authentication import CognitiveServicesCredentials

region = "westcentralus"
key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

credentials = CognitiveServicesCredentials(key)
client = ComputerVisionAPI(region, credentials)
```

[ComputerVisionAPI][ref_computervisionclient] 클라이언트 개체가 있어야 다음 작업을 사용할 수 있습니다.

### <a name="analyze-an-image"></a>이미지 분석

[`analyze_image`][ref_computervisionclient_analyze_image]로 특정 기능에 대한 이미지를 분석할 수 있습니다. [`visual_features`][ref_computervision_model_visualfeatures] 속성을 사용하여 이미지에서 수행하는 분석의 형식을 설정합니다. 일반 값은 `VisualFeatureTypes.tags` 및 `VisualFeatureTypes.description`입니다.

```Python
url = "https://upload.wikimedia.org/wikipedia/commons/thumb/1/12/Broadway_and_Times_Square_by_night.jpg/450px-Broadway_and_Times_Square_by_night.jpg"

image_analysis = client.analyze_image(url,visual_features=[VisualFeatureTypes.tags])

for tag in image_analysis.tags:
    print(tag)
```

### <a name="get-subject-domain-list"></a>주체 도메인 목록 가져오기

[`list_models`][ref_computervisionclient_list_models]로 이미지를 분석하는 데 사용되는 주체 도메인을 검토합니다. 이러한 도메인 이름은 [도메인 기준으로 이미지를 분석](#analyze-an-image-by-domain)하는 경우 사용됩니다. `landmarks`가 도메인의 한 예입니다.

```Python
models = client.list_models()

for x in models.models_property:
    print(x)
```

### <a name="analyze-an-image-by-domain"></a>도메인 기준 이미지 분석

[`analyze_image_by_domain`][ref_computervisionclient_analyze_image_by_domain]으로 주체 도메인 기준으로 이미지를 분석할 수 있습니다. 올바른 도메인 이름을 사용하려면 [지원되는 주체 도메인의 목록](#get-subject-domain-list)을 가져옵니다.  

```Python
# type of prediction
domain = "landmarks"

# Public domain image of Eiffel tower
url = "https://images.pexels.com/photos/338515/pexels-photo-338515.jpeg"

# English language response
language = "en"

analysis = client.analyze_image_by_domain(domain, url, language)

for landmark in analysis.result["landmarks"]:
    print(landmark["name"])
    print(landmark["confidence"])
```

### <a name="get-text-description-of-an-image"></a>이미지의 텍스트 설명 가져오기

[`describe_image`][ref_computervisionclient_describe_image]로 이미지의 언어 기반 텍스트 설명을 가져올 수 있습니다. 이미지와 연결된 키워드에 대한 텍스트 분석을 수행하는 경우 `max_description` 속성으로 몇 가지 설명을 요청합니다. 다음 이미지에 대한 텍스트 설명의 예제에는 `a train crossing a bridge over a body of water`, `a large bridge over a body of water` 및 `a train crossing a bridge over a large body of water`가 포함됩니다.

```Python
domain = "landmarks"
url = "http://www.public-domain-photos.com/free-stock-photos-4/travel/san-francisco/golden-gate-bridge-in-san-francisco.jpg"
language = "en"
max_descriptions = 3

analysis = client.describe_image(url, max_descriptions, language)

for caption in analysis.captions:
    print(caption.text)
    print(caption.confidence)
```

### <a name="get-text-from-image"></a>이미지에서 텍스트 가져오기

이미지에서 필기 또는 인쇄된 텍스트를 가져올 수 있습니다. 이를 위해서는 SDK에 대한 두 호출인 [`recognize_text`][ref_computervisionclient_recognize_text] 및 [`get_text_operation_result`][ref_computervisionclient_get_text_operation_result]가 필요합니다. recognize_text에 대한 호출은 비동기적입니다. get_text_operation_result 호출의 결과에서 텍스트 데이터를 추출하기 전에 첫 번째 호출이 [`TextOperationStatusCodes`][ref_computervision_model_textoperationstatuscodes]로 완료되었는지 확인해야 합니다. 결과에는 텍스트뿐만 아니라 텍스트에 대한 경계 상자 좌표가 포함됩니다. 

```Python
# import models
from azure.cognitiveservices.vision.computervision.models import TextRecognitionMode
from azure.cognitiveservices.vision.computervision.models import TextOperationStatusCodes

url = "https://azurecomcdn.azureedge.net/cvt-1979217d3d0d31c5c87cbd991bccfee2d184b55eeb4081200012bdaf6a65601a/images/shared/cognitive-services-demos/read-text/read-1-thumbnail.png"
mode = TextRecognitionMode.handwritten
raw = True
custom_headers = None
numberOfCharsInOperationId = 36

# SDK call
rawHttpResponse = client.recognize_text(url, mode, custom_headers,  raw)

# Get ID from returned headers
operationLocation = rawHttpResponse.headers["Operation-Location"]
idLocation = len(operationLocation) - numberOfCharsInOperationId
operationId = operationLocation[idLocation:]

# SDK call
result = client.get_text_operation_result(operationId)

# Get data
if result.status == TextOperationStatusCodes.succeeded:

    for line in result.recognition_result.lines:
        print(line.text)
        print(line.bounding_box)
```

### <a name="generate-thumbnail"></a>썸네일 생성

[`generate_thumbnail`][ref_computervisionclient_generate_thumbnail]로 이미지의 썸네일(JPG)을 생성할 수 있습니다. 썸네일이 원래 이미지와 동일한 비율일 필요는 없습니다. 

이 예제를 사용하려면 **Pillow**를 설치합니다.

```bash
pip install Pillow
``` 

Pillow가 설치되면 다음 코드 예제에서 패키지를 사용하여 썸네일 이미지를 생성합니다.

```Python
# Pillow package
from PIL import Image

# IO package to create local image
import io

width = 50
height = 50
url = "http://www.public-domain-photos.com/free-stock-photos-4/travel/san-francisco/golden-gate-bridge-in-san-francisco.jpg"

thumbnail = client.generate_thumbnail(width, height, url)

for x in thumbnail:
    image = Image.open(io.BytesIO(x))

image.save('thumbnail.jpg')
```

## <a name="troubleshooting"></a>문제 해결

### <a name="general"></a>일반

Python SDK를 사용하여 [ComputerVisionAPI][ref_computervisionclient] 클라이언트 개체와 상호 작용하는 경우 오류를 반환하는 데 [`ComputerVisionErrorException`][ref_computervision_computervisionerrorexception] 클래스가 사용됩니다. 서비스에서 반환되는 오류는 REST API 요청에 대해 반환되는 동일한 HTTP 상태 코드에 해당합니다.

예를 들어, 잘못된 키를 사용하여 이미지를 분석하려는 경우 `401` 오류가 반환됩니다. 다음 코드 조각에서 [오류][ref_httpfailure]는 예외를 catch하고 오류에 대한 추가 정보를 표시하여 적절히 처리됩니다.

```Python

domain = "landmarks"
url = "http://www.public-domain-photos.com/free-stock-photos-4/travel/san-francisco/golden-gate-bridge-in-san-francisco.jpg"
language = "en"
max_descriptions = 3

try:
    analysis = client.describe_image(url, max_descriptions, language)

    for caption in analysis.captions:
        print(caption.text)
        print(caption.confidence)
except HTTPFailure as e:
    if e.status_code == 401:
        print("Error unauthorized. Make sure your key and region are correct.")
    else:
        raise
```

### <a name="handle-transient-errors-with-retries"></a>재시도를 통한 일시적인 오류 처리

[ComputerVisionAPI][ref_computervisionclient] 클라이언트를 사용하는 동안 서비스에서 적용되는 [속도 제한][computervision_request_units] 또는 네트워크 중단과 같은 다른 일시적인 문제가 발생할 수도 있습니다. 이러한 유형의 오류를 처리하는 방법에 대한 내용은 클라우드 디자인 패턴 가이드의 [다시 시도 패턴][azure_pattern_retry] 및 관련 [회로 차단기 패턴][azure_pattern_circuit_breaker]을 참조하세요.

### <a name="more-sample-code"></a>추가 샘플 코드

여러 Computer Vision Python SDK 샘플을 SDK의 GitHub 리포지토리에서 확인할 수 있습니다. 이러한 샘플에는 Computer Vision을 사용하는 동안 흔히 발생하는 추가 시나리오에 대한 예제 코드가 들어 있습니다.

* [recognize_text][recognize-text]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [이미지에 콘텐츠 태그 적용](../concept-tagging-images.md)

<!-- LINKS -->
[pip]: https://pypi.org/project/pip/
[python]: https://www.python.org/downloads/

[azure_cli]: https://docs.microsoft.com/cli/azure
[azure_pattern_circuit_breaker]: https://docs.microsoft.com/azure/architecture/patterns/circuit-breaker
[azure_pattern_retry]: https://docs.microsoft.com/azure/architecture/patterns/retry
[azure_portal]: https://portal.azure.com
[azure_sub]: https://azure.microsoft.com/free/

[cloud_shell]: https://docs.microsoft.com/azure/cloud-shell/overview

[venv]: https://docs.python.org/3/library/venv.html
[virtualenv]: https://virtualenv.pypa.io

[source_code]: https://github.com/Azure/azure-sdk-for-python/tree/master/azure-cognitiveservices-vision-computervision

[pypi_computervision]:https://pypi.org/project/azure-cognitiveservices-vision-computervision/
[pypi_pillow]:https://pypi.org/project/Pillow/

[ref_computervision_sdk]: https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision?view=azure-python
[ref_computervision_computervisionerrorexception]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.models.computervisionerrorexception?view=azure-python
[ref_httpfailure]: https://docs.microsoft.com/python/api/msrest/msrest.exceptions.httpoperationerror?view=azure-python


[computervision_resource]: https://docs.microsoft.com/azure/cognitive-services/computer-vision/vision-api-how-to-topics/howtosubscribe

[computervision_docs]: https://docs.microsoft.com/azure/cognitive-services/computer-vision/home

[ref_computervisionclient]: https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python


[ref_computervisionclient_analyze_image]: https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python#analyze-image-url--visual-features-none--details-none--language--en---custom-headers-none--raw-false----operation-config-
[ref_computervisionclient_list_models]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python#list-models-custom-headers-none--raw-false----operation-config-
[ref_computervisionclient_analyze_image_by_domain]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python#analyze-image-by-domain-model--url--language--en---custom-headers-none--raw-false----operation-config-
[ref_computervisionclient_describe_image]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python#describe-image-url--max-candidates--1---language--en---custom-headers-none--raw-false----operation-config-
[ref_computervisionclient_recognize_text]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python#recognize-text-url--mode--custom-headers-none--raw-false----operation-config-
[ref_computervisionclient_get_text_operation_result]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python#get-text-operation-result-operation-id--custom-headers-none--raw-false----operation-config-
[ref_computervisionclient_generate_thumbnail]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.computervisionapi?view=azure-python#generate-thumbnail-width--height--url--smart-cropping-false--custom-headers-none--raw-false--callback-none----operation-config-


[ref_computervision_model_visualfeatures]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.models.visualfeaturetypes?view=azure-python

[ref_computervision_model_textoperationstatuscodes]:https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-computervision/azure.cognitiveservices.vision.computervision.models.textoperationstatuscodes?view=azure-python

[computervision_request_units]:https://azure.microsoft.com/pricing/details/cognitive-services/computer-vision/

[recognize-text]:https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/vision/computer_vision_samples.py


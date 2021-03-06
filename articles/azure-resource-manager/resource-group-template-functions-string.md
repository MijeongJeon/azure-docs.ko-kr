---
title: Azure Resource Manager 템플릿 함수 - 문자열 | Microsoft Docs
description: Azure Resource Manager 템플릿에서 문자열 작업을 수행하는 데 사용할 수 있는 함수에 대해 설명합니다.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/11/2019
ms.author: tomfitz
ms.openlocfilehash: c35352c47edb4f34100501ac791c84108fa9ac17
ms.sourcegitcommit: 5fbca3354f47d936e46582e76ff49b77a989f299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2019
ms.locfileid: "57762843"
---
# <a name="string-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿용 문자열 함수

Resource Manager는 문자열 작업을 위한 다음 함수를 제공합니다.

* [base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [contains](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [empty](#empty)
* [endsWith](#endswith)
* [first](#first)
* [guid](#guid)
* [indexOf](#indexof)
* [last](#last)
* [lastIndexOf](#lastindexof)
* [length](#length)
* [newGuid](#newguid)
* [padLeft](#padleft)
* [replace](#replace)
* [skip](#skip)
* [split](#split)
* [startsWith](#startswith)
* [string](#string)
* [substring](#substring)
* [take](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [trim](#trim)
* [uniqueString](#uniquestring)
* [uri](#uri)
* [uriComponent](#uricomponent)
* [uriComponentToString](#uricomponenttostring)
* [utcNow](#utcnow)

## <a name="base64"></a>base64

`base64(inputString)`

입력 문자열의 base64 표현을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| inputString |예 |string |base64 표현으로 반환할 값입니다. |

### <a name="return-value"></a>반환 값

Base64 표현을 포함하는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json)에서는 base64 함수를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| base64Output | 문자열 | b25lLCB0d28sIHRocmVl |
| toStringOutput | 문자열 | one, two, three |
| toJsonOutput | Object | {“one”: “a”, “two”: “b”} |

## <a name="base64tojson"></a>base64ToJson

`base64tojson`

base64 표현을 JSON 개체로 변환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| base64Value |예 |string |JSON 개체로 변환할 base64 표현입니다. |

### <a name="return-value"></a>반환 값

JSON 개체입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json)에서는 base64ToJson 함수를 사용하여 base64 값을 변환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| base64Output | 문자열 | b25lLCB0d28sIHRocmVl |
| toStringOutput | 문자열 | one, two, three |
| toJsonOutput | Object | {“one”: “a”, “two”: “b”} |

## <a name="base64tostring"></a>base64ToString

`base64ToString(base64Value)`

base64 표현을 문자열로 변환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| base64Value |예 |string |문자열로 변환할 base64 표현입니다. |

### <a name="return-value"></a>반환 값

변환된 base64 값의 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json)에서는 base64ToString 함수를 사용하여 base64 값을 변환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| base64Output | 문자열 | b25lLCB0d28sIHRocmVl |
| toStringOutput | 문자열 | one, two, three |
| toJsonOutput | Object | {“one”: “a”, “two”: “b”} |

## <a name="concat"></a>concat

`concat (arg1, arg2, arg3, ...)`

여러 문자열 값을 결합하고 연결된 문자열을 반환하거나 여러 배열을 결합하고 연결된 배열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |문자열 또는 배열 |연결할 첫 번째 값입니다. |
| 추가 인수 |아니요 |string |연결할 추가 값(순서대로)입니다. |

### <a name="return-value"></a>반환 값
연결된 값의 문자열 또는 배열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-string.json)에서는 2개의 문자열 값을 결합하고 연결된 문자열을 반환하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| concatOutput | 문자열 | prefix-5yj4yjf5mbg72 |

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-array.json)에서는 두 개의 배열을 결합하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| return | 배열 | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

## <a name="contains"></a>contains

`contains (container, itemToFind)`

배열에 값이 포함되는지, 개체에 키가 포함되는지 또는 문자열에 하위 문자열이 포함되는지를 확인합니다. 문자열 비교에서는 대/소문자를 구분합니다. 그러나 개체에 키가 포함되어 있는지를 테스트할 때는 비교에서 대/소문자를 구분하지 않습니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| container |예 |배열, 개체 또는 문자열 |찾을 값을 포함하는 값입니다. |
| itemToFind |예 |문자열 또는 int |찾을 값입니다. |

### <a name="return-value"></a>반환 값

항목이 있으면 **True**이고, 항목이 없으면 **False**입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/contains.json)에서는 여러 다른 형식의 contains를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| stringTrue | Bool | True |
| stringFalse | Bool | False |
| objectTrue | Bool | True |
| objectFalse | Bool | False |
| arrayTrue | Bool | True |
| arrayFalse | Bool | False |

## <a name="datauri"></a>dataUri

`dataUri(stringToConvert)`

값을 데이터 URI로 변환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToConvert |예 |string |데이터 URI로 변환할 값입니다. |

### <a name="return-value"></a>반환 값

데이터 URI로 형식이 지정된 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/datauri.json)에서는 값을 데이터 URI로 변환하고 데이터 URI를 문자열로 변환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| dataUriOutput | 문자열 | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | 문자열 | Hello, World! |

## <a name="datauritostring"></a>dataUriToString

`dataUriToString(dataUriToConvert)`

데이터 URI로 형식이 지정된 값을 문자열로 변환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |예 |string |변환할 데이터 URI 값입니다. |

### <a name="return-value"></a>반환 값

변환된 값을 포함하는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/datauri.json)에서는 값을 데이터 URI로 변환하고 데이터 URI를 문자열로 변환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| dataUriOutput | 문자열 | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | 문자열 | Hello, World! |

## <a name="empty"></a>empty

`empty(itemToTest)`

배열, 개체 또는 문자열이 비어 있는지를 확인합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| itemToTest |예 |배열, 개체 또는 문자열 |비어 있는지 확인할 값입니다. |

### <a name="return-value"></a>반환 값

값이 비어 있으면 **True**를 반환하고 비어 있지 않으면 **False**를 반환합니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/empty.json)에서는 배열, 개체 및 문자열이 비어 있는지 여부를 확인합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| arrayEmpty | Bool | True |
| objectEmpty | Bool | True |
| stringEmpty | Bool | True |

## <a name="endswith"></a>endsWith

`endsWith(stringToSearch, stringToFind)`

문자열이 값으로 끝나는지 여부를 결정합니다. 비교는 대/소문자를 구분합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |찾을 값을 포함하는 값입니다. |
| stringToFind |예 |string |찾을 값입니다. |

### <a name="return-value"></a>반환 값

마지막 문자 또는 문자열의 문자가 값과 일치하면 **True**이고, 일치하지 않으면 **False**입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/startsendswith.json)에서는 startsWith 및 endsWith 함수를 사용하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| startsTrue | Bool | True |
| startsCapTrue | Bool | True |
| startsFalse | Bool | False |
| endsTrue | Bool | True |
| endsCapTrue | Bool | True |
| endsFalse | Bool | False |

## <a name="first"></a>first

`first(arg1)`

문자열의 첫 번째 문자 또는 배열의 첫 번째 요소를 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |첫 번째 요소 또는 문자를 검색할 값입니다. |

### <a name="return-value"></a>반환 값

배열의 첫 번째 문자의 문자열 또는 첫 번째 요소의 형식(문자열, int, 배열 또는 개체)입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/first.json)에서는 배열 및 문자열에 첫 번째 함수를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| arrayOutput | 문자열 | one |
| stringOutput | 문자열 | O |

## <a name="guid"></a>GUID

`guid (baseString, ...)`

매개 변수로 제공된 값을 기반으로 전역 고유 식별자 형식으로 값을 만듭니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| baseString |예 |string |해시 함수에서 GUID를 만드는 데 사용되는 값입니다. |
| 필요에 따라 추가하는 매개 변수 |아니요 |string |고유성 수준을 지정하는 값을 만들기 위해 필요한 만큼 문자열을 추가할 수 있습니다. |

### <a name="remarks"></a>설명

이 함수는 전역 고유 식별자 형식으로 값을 만들어야 할 때 유용합니다. 결과의 고유성 범위를 제한하는 매개 변수 값을 제공합니다. 구독, 리소스 그룹 또는 배포까지 해당 이름이 고유한지 여부를 지정할 수 있습니다.

반환된 된 값이 임의의 문자열이 있지만 매개 변수에 대 한 해시 함수 결과 대신 아닙니다. 반환된 값은 36자입니다. 전역적으로 고유하지 않습니다. 매개 변수를 해시 값을 기반으로 하지 않는 하는 새 GUID를 만들려면 사용 합니다 [newGuid](#newguid) 함수입니다.

다음 예제에서는 guid를 사용하여 일반적으로 사용하는 수준에 대해 고유한 값을 만드는 방법을 보여 줍니다.

구독에 범위가 지정된 고유함

```json
"[guid(subscription().subscriptionId)]"
```

리소스 그룹에 범위가 지정된 고유함

```json
"[guid(resourceGroup().id)]"
```

리소스 그룹의 배포에 범위가 지정된 고유함

```json
"[guid(resourceGroup().id, deployment().name)]"
```

### <a name="return-value"></a>반환 값

전 세계적으로 고유한 식별자의 형식으로 된 36자를 포함하는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/guid.json)은 guid의 결과를 반환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {},
    "resources": [],
    "outputs": {
        "guidPerSubscription": {
            "value": "[guid(subscription().subscriptionId)]",
            "type": "string"
        },
        "guidPerResourceGroup": {
            "value": "[guid(resourceGroup().id)]",
            "type": "string"
        },
        "guidPerDeployment": {
            "value": "[guid(resourceGroup().id, deployment().name)]",
            "type": "string"
        }
    }
}
```

## <a name="indexof"></a>indexof

`indexOf(stringToSearch, stringToFind)`

문자열 내 값의 첫 번째 위치를 반환합니다. 비교는 대/소문자를 구분합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |찾을 값을 포함하는 값입니다. |
| stringToFind |예 |string |찾을 값입니다. |

### <a name="return-value"></a>반환 값

찾을 항목의 위치를 나타내는 정수입니다. 값은 0부터 시작합니다. 항목이 없는 경우 -1이 반환됩니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/indexof.json)에서는 indexOf 및 lastIndexOf 함수를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

## <a name="last"></a>last

`last (arg1)`

문자열의 마지막 문자 또는 배열의 마지막 요소를 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |마지막 요소 또는 문자를 검색할 값입니다. |

### <a name="return-value"></a>반환 값

배열의 마지막 문자의 문자열 또는 마지막 요소의 형식(문자열, int, 배열 또는 개체)입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/last.json)에서는 배열 및 문자열에 최근 함수를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| arrayOutput | 문자열 | three |
| stringOutput | 문자열 | e |

## <a name="lastindexof"></a>lastindexof

`lastIndexOf(stringToSearch, stringToFind)`

문자열 내 값의 마지막 위치를 반환합니다. 비교는 대/소문자를 구분합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |찾을 값을 포함하는 값입니다. |
| stringToFind |예 |string |찾을 값입니다. |

### <a name="return-value"></a>반환 값

찾을 항목의 마지막 위치를 나타내는 정수입니다. 값은 0부터 시작합니다. 항목이 없는 경우 -1이 반환됩니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/indexof.json)에서는 indexOf 및 lastIndexOf 함수를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

## <a name="length"></a>length

`length(string)`

문자열의 문자 수 또는 배열의 요소 수를 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| arg1 |예 |배열 또는 문자열 |요소 수를 가져오는 데 사용할 배열 또는 문자 수를 가져오는 데 사용할 문자열입니다. |

### <a name="return-value"></a>반환 값

int입니다. 

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/length.json)에서는 배열 및 문자열에 length를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

## <a name="newguid"></a>newGuid

`newGuid()`

전역적으로 고유 식별자 형식의 값을 반환 합니다. **이 함수는 매개 변수에 대 한 기본값인 에서만 사용 수 있습니다.**

### <a name="remarks"></a>설명

매개 변수의 기본값만 식 내에서이 함수를 사용할 수 있습니다. 템플릿에서 다른 곳에이 함수를 사용 하 여 오류를 반환 합니다. 함수를 호출할 때마다 다른 값을 반환 하기 때문에 템플릿의 다른 부분에서 허용 되지 않습니다. 동일한 매개 변수를 사용 하 여 동일한 템플릿에 배포 같은 결과 안정적으로 생성 하지 않습니다.

NewGuid 함수에서 다른 합니다 [guid](#guid) 매개 변수를 사용 하지 때문에 작동 합니다. 동일한 매개 변수를 사용 하 여 guid를 호출할 때마다 동일한 식별자를 반환 됩니다. 특정 환경에 동일한 GUID를 안정적으로 생성 해야 하는 경우에 guid를 사용 합니다. 매번 테스트 환경에 리소스 배포와 같은 다른 식별자가 필요한 경우 newGuid를 사용 합니다.

사용 하는 경우는 [이전 성공적인 배포를 다시 배포 하는 옵션](resource-group-template-deploy-rest.md#redeploy-when-deployment-fails), newGuid를 사용 하는 매개 변수를 포함 하는 이전 배포를 매개 변수 다시 평가 되지 않습니다. 대신 이전 배포에서 매개 변수 값을 롤백 배포에서 자동으로 재사용 됩니다.

테스트 환경에서 반복적으로 짧은 시간 동안에 존재 하는 리소스를 배포 해야 할 수 있습니다. 고유한 이름을 생성 하는 대신 사용 하 여 newGuid를 사용할 수 있습니다 [uniqueString](#uniquestring) 고유 이름을 만듭니다.

기본값에 대 한 newGuid 함수에 의존 하는 템플릿을 다시 배포 주의 해야 합니다. 다시 배포 하 고 매개 변수 값을 제공 하지는 다시 평가 됩니다. 새로 만들어야 하는 것이 아니라 기존 리소스를 업데이트 하려는 경우 이전 배포에서 매개 변수 값에 전달 합니다.

### <a name="return-value"></a>반환 값

전 세계적으로 고유한 식별자의 형식으로 된 36자를 포함하는 문자열입니다.

### <a name="examples"></a>예

다음 예제 템플릿은 새 식별자를 사용 하 여 매개 변수를 표시 합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "guidValue": {
            "type": "string",
            "defaultValue": "[newGuid()]"
        }
    },
    "resources": [
    ],
    "outputs": {
        "guidOutput": {
            "type": "string",
            "value": "[parameters('guidValue')]"
        }
    }
}
```

출력 앞의 예제에서 각 배포에 대 한 다르지만 비슷합니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| guidOutput | 문자열 | b76a51fc-bd72-4a77-b9a2-3c29e7d2e551 |

다음 예제에서는 저장소 계정에 대 한 고유한 이름을 만들기 위해 newGuid 함수를 사용 합니다. 이 템플릿은 저장소 계정 짧은 시간 동안 존재 및 다시 배포 하지는 테스트 환경용 적합할 수 있습니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "guidValue": {
            "type": "string",
            "defaultValue": "[newGuid()]"
        }
    },
    "variables": {
        "storageName": "[concat('storage', uniqueString(parameters('guidValue')))]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[variables('storageName')]",
            "location": "West US",
            "apiVersion": "2018-07-01",
            "sku":{
                "name": "Standard_LRS"
            },
            "kind": "StorageV2",
            "properties": {}
        }
    ],
    "outputs": {
        "nameOutput": {
            "type": "string",
            "value": "[variables('storageName')]"
        }
    }
}
```

출력 앞의 예제에서 각 배포에 대 한 다르지만 비슷합니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| nameOutput | 문자열 | storagenziwvyru7uxie |


## <a name="padleft"></a>padLeft

`padLeft(valueToPad, totalLength, paddingCharacter)`

지정된 총 길이에 도달할 때까지 왼쪽에 문자를 추가하여 오른쪽 맞추어진 문자열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| valueToPad |예 |문자열 또는 int |오른쪽으로 맞출 값입니다. |
| totalLength |예 |int |반환된 문자열에서 문자의 총수입니다. |
| paddingCharacter |아니요 |단일 문자 |총 길이에 도달할 때까지 왼쪽 여백에 사용되는 문자입니다. 기본값은 공백입니다. |

원래 문자열이 채울 문자 수보다 긴 경우 문자가 추가되지 않습니다.

### <a name="return-value"></a>반환 값

최소한 지정된 문자의 수를 포함하는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/padleft.json)에서는 문자열이 총 문자 수에 도달할 때까지 0 문자를 추가하여 사용자가 제공한 매개 변수 값을 채우는 방법을 보여줍니다. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| stringOutput | 문자열 | 0000000123 |

## <a name="replace"></a>바꾸기

`replace(originalString, oldString, newString)`

다른 문자열로 대체한 어떤 문자열의 인스턴스를 포함한 새 문자열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalString |예 |string |다른 문자열로 대체한 어떤 문자열의 인스턴스를 포함하는 값입니다. |
| oldString |예 |string |원래 문자열에서 제거할 문자열입니다. |
| newString |예 |string |제거된 문자열 대신 추가할 문자열입니다. |

### <a name="return-value"></a>반환 값

문자가 대체된 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/replace.json)에서는 사용자가 제공한 문자열에서 모든 대시를 제거하는 방법 및 문자열의 일부를 다른 문자열로 대체하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| firstOutput | 문자열 | 1231231234 |
| secodeOutput | 문자열 | 123-123-xxxx |

## <a name="skip"></a>skip

`skip(originalValue, numberToSkip)`

지정된 문자 수 이후의 모든 문자를 포함하는 문자열 또는 지정된 요소 수 이후의 모든 요소를 포함하는 배열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalValue |예 |배열 또는 문자열 |건너뛰는 데 사용할 배열 또는 문자열입니다. |
| numberToSkip |예 |int |건너뛸 요소 또는 문자 수입니다. 이 값이 0 이하이면 값의 모든 요소 또는 문자가 반환됩니다. 이 값이 배열 또는 문자열의 길이보다 크면 빈 배열 또는 문자열이 반환됩니다. |

### <a name="return-value"></a>반환 값

배열 또는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/skip.json)에서는 배열에서 지정된 요소 수 및 문자열에서 지정된 수의 문자를 건너뜁니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| arrayOutput | 배열 | ["three"] |
| stringOutput | 문자열 | two three |

## <a name="split"></a>split

`split(inputString, delimiter)`

지정된 구분 기호로 구분되는 입력 문자열의 부분 문자열을 포함하는 문자열의 배열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| inputString |예 |string |분할할 문자열입니다. |
| 구분 기호 |예 |문자열 또는 문자열 배열 |문자열 분할에 사용할 구분 기호입니다. |

### <a name="return-value"></a>반환 값

문자열 배열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/split.json)에서는 쉼표를 사용하여 또는 쉼표 또는 세미콜론을 사용하여 입력 문자열을 분할합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| firstOutput | 배열 | [“one”, “two”, “three”] |
| secondOutput | 배열 | [“one”, “two”, “three”] |

## <a name="startswith"></a>startswith

`startsWith(stringToSearch, stringToFind)`

문자열이 값으로 시작하는지 여부를 결정합니다. 비교는 대/소문자를 구분합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToSearch |예 |string |찾을 값을 포함하는 값입니다. |
| stringToFind |예 |string |찾을 값입니다. |

### <a name="return-value"></a>반환 값

첫 번째 문자 또는 문자열의 문자가 값과 일치하면 **True**이고, 일치하지 않으면 **False**입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/startsendswith.json)에서는 startsWith 및 endsWith 함수를 사용하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| startsTrue | Bool | True |
| startsCapTrue | Bool | True |
| startsFalse | Bool | False |
| endsTrue | Bool | True |
| endsCapTrue | Bool | True |
| endsFalse | Bool | False |

## <a name="string"></a>문자열

`string(valueToConvert)`

지정된 값을 문자열로 변환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| valueToConvert |예 | 모두 |문자열로 변환할 값입니다. 개체 및 배열을 비롯하여 모든 값 형식을 변환할 수 있습니다. |

### <a name="return-value"></a>반환 값

변환된 값의 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/string.json)에서는 다른 형식의 값을 문자열로 변환하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| objectOutput | 문자열 | {“valueA”:10,“valueB”:“Example Text”} |
| arrayOutput | 문자열 | [“a”,“b”,“c”] |
| intOutput | 문자열 | 5 |

## <a name="substring"></a>substring

`substring(stringToParse, startIndex, length)`

지정된 문자 위치에서 시작하고 지정한 개수의 문자를 포함하는 부분 문자열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToParse |예 |string |부분 문자열을 추출할 원래 문자열입니다. |
| startIndex |아니요 |int |부분 문자열의 0부터 시작하는 문자 위치입니다. |
| length |아니요 |int |부분 문자열에 대한 문자 수입니다. 문자열 내 위치를 참조해야 합니다. 0 이상이어야 합니다. |

### <a name="return-value"></a>반환 값

하위 문자열입니다. 또는 길이가 0인 경우 빈 문자열입니다.

### <a name="remarks"></a>설명

함수는 부분 문자열이 문자열의 끝을 넘어 확장되거나 길이가 0보다 작은 경우 실패합니다. 다음 예제는 "인덱스 및 길이 매개 변수는 문자열 내 위치를 참조해야 합니다. 인덱스 매개 변수: '0', 길이 매개 변수: '11', 문자열 매개 변수의 길이: '10'.".

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/substring.json)에서는 매개 변수에서 하위 문자열을 추출합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| substringOutput | 문자열 | two |

## <a name="take"></a>take

`take(originalValue, numberToTake)`

문자열 시작부터 지정된 수의 문자를 포함하는 문자열 또는 배열 시작부터 지정된 수의 요소를 포함하는 배열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| originalValue |예 |배열 또는 문자열 |요소를 가져올 배열 또는 문자열입니다. |
| numberToTake |예 |int |수락할 요소 또는 문자의 수입니다. 이 값이 0 이하이면 빈 배열 또는 문자열이 반환됩니다. 지정된 배열 또는 문자열의 길이보다 크면 배열 또는 문자열의 모든 요소가 반환됩니다. |

### <a name="return-value"></a>반환 값

배열 또는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/take.json)에서는 배열에서 지정된 수의 요소 및 문자열의 문자를 가져옵니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| arrayOutput | 배열 | ["one", "two"] |
| stringOutput | 문자열 | on |

## <a name="tolower"></a>toLower

`toLower(stringToChange)`

지정된 문자열을 소문자로 변환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToChange |예 |string |소문자로 변환할 값입니다. |

### <a name="return-value"></a>반환 값

소문자로 변환된 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/tolower.json)에서는 매개 변수 값을 소문자 및 대문자로 변환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| toLowerOutput | 문자열 | one two three |
| toUpperOutput | 문자열 | ONE TWO THREE |

## <a name="toupper"></a>toUpper

`toUpper(stringToChange)`

지정된 문자열을 대문자로 변환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToChange |예 |string |대문자로 변환할 값입니다. |

### <a name="return-value"></a>반환 값

대문자로 변환된 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/tolower.json)에서는 매개 변수 값을 소문자 및 대문자로 변환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| toLowerOutput | 문자열 | one two three |
| toUpperOutput | 문자열 | ONE TWO THREE |

## <a name="trim"></a>trim

`trim (stringToTrim)`

지정된 문자열에서 모든 선행 및 후행 공백 문자를 제거합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToTrim |예 |string |자를 값입니다. |

### <a name="return-value"></a>반환 값

선행 및 후행 공백 문자가 없는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/trim.json)에서는 매개 변수에서 공백 문자를 자릅니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| return | 문자열 | one two three |

## <a name="uniquestring"></a>uniqueString

`uniqueString (baseString, ...)`

매개 변수로 제공된 값을 기반으로 결정 해시 문자열을 만듭니다. 

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| baseString |예 |string |고유한 문자열을 만들기 위해 해시 함수에서 사용되는 값입니다. |
| 필요에 따라 추가하는 매개 변수 |아니요 |string |고유성 수준을 지정하는 값을 만들기 위해 필요한 만큼 문자열을 추가할 수 있습니다. |

### <a name="remarks"></a>설명

이 함수는 리소스의 고유한 이름을 만들어야 할 때 유용합니다. 결과의 고유성 범위를 제한하는 매개 변수 값을 제공합니다. 구독, 리소스 그룹 또는 배포까지 해당 이름이 고유한지 여부를 지정할 수 있습니다. 

반환된 값은 임의 문자열이 아닌 해시 함수의 결과입니다. 반환된 값은 13자입니다. 전역적으로 고유하지 않습니다. 의미있는 이름을 만들기 위해 해당 값과 명명 규칙의 접두사를 결합할 수도 있습니다. 다음 예제에서는 반환된 값의 형식을 보여 줍니다. 실제 값은 제공된 매개 변수에 따라 달라집니다.

    tcvhiyu5h2o5o

다음 예제에서는 uniqueString를 사용하여 일반적으로 사용하는 수준에 대해 고유한 값을 만드는 방법을 보여 줍니다.

구독에 범위가 지정된 고유함

```json
"[uniqueString(subscription().subscriptionId)]"
```

리소스 그룹에 범위가 지정된 고유함

```json
"[uniqueString(resourceGroup().id)]"
```

리소스 그룹의 배포에 범위가 지정된 고유함

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

다음 예제에서는 리소스 그룹에 따라 저장소 계정에 고유한 이름을 만드는 방법을 보여 줍니다. 리소스 그룹의 내부에서 같은 방식으로 생성된 경우 이름은 고유하지 않습니다.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

사용할 수 있습니다, 템플릿을 배포 하 고 리소스를 업데이트 하려면 인하지 않으려는 될 때마다 새 고유 이름을 생성 해야 하는 경우는 [utcNow](#utcnow) uniqueString 사용 하 여 함수입니다. 이 방법은 테스트 환경에서 사용할 수 있습니다. 예를 들어 참조 [utcNow](#utcNow)합니다.

### <a name="return-value"></a>반환 값

13개의 문자를 포함하는 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uniquestring.json)에서는 uniquestring에서 결과를 반환합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

## <a name="uri"></a>uri

`uri (baseUri, relativeUri)`

baseUri와 relativeUri 문자열을 결합하여 절대 URI를 만듭니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| baseUri |예 |string |기본 uri 문자열입니다. |
| relativeUri |예 |string |기본 uri 문자열에 추가할 상대 uri 문자열입니다. |

**baseUri** 매개 변수에 대한 값은 특정 파일을 포함할 수 있지만 URI를 생성하는 경우 기본 경로만 사용됩니다. 예를 들어 `http://contoso.com/resources/azuredeploy.json`을 baseUri 매개 변수로 전달하면 기본 URI는 `http://contoso.com/resources/`가 됩니다.

### <a name="return-value"></a>반환 값

기본 및 상대 값에 대한 절대 URI를 나타내는 문자열입니다.

### <a name="examples"></a>예

다음 예제에서는 부모 템플릿의 값을 기반으로 중첩된 템플릿에 대한 링크를 생성하는 방법을 보여 줍니다.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json)에서는 uri, uriComponent 및 uriComponentToString를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| uriOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | 문자열 | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |

## <a name="uricomponent"></a>uriComponent

`uricomponent(stringToEncode)`

URI를 인코딩합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| stringToEncode |예 |string |인코딩할 값입니다. |

### <a name="return-value"></a>반환 값

URI로 인코딩된 값의 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json)에서는 uri, uriComponent 및 uriComponentToString를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| uriOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | 문자열 | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |

## <a name="uricomponenttostring"></a>uriComponentToString

`uriComponentToString(uriEncodedString)`

URI로 인코딩된 값의 문자열을 반환합니다.

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| uriEncodedString |예 |string |문자열로 변환할 URI 인코딩 값입니다. |

### <a name="return-value"></a>반환 값

URI로 인코딩된 값의 디코딩된 문자열입니다.

### <a name="examples"></a>예

다음 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json)에서는 uri, uriComponent 및 uriComponentToString를 사용하는 방법을 보여줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| uriOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | 문자열 | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | 문자열 | http://contoso.com/resources/nested/azuredeploy.json |

## <a name="utcnow"></a>utcNow

`utcNow(format)`

지정 된 형식의 현재 UTC 날짜/시간 값을 반환합니다. 서식을 제공 하는 경우 ISO 8601 (yyyyMMddTHHmmssZ) 형식으로 사용 됩니다. **이 함수는 매개 변수에 대 한 기본값인 에서만 사용 수 있습니다.**

### <a name="parameters"></a>매개 변수

|  매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| format |아닙니다. |문자열 |문자열로 변환할 URI 인코딩 값입니다. 사용 하 여 [표준 형식 문자열](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) 하거나 [사용자 지정 형식 문자열](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings)합니다. |

### <a name="remarks"></a>설명

매개 변수의 기본값만 식 내에서이 함수를 사용할 수 있습니다. 템플릿에서 다른 곳에이 함수를 사용 하 여 오류를 반환 합니다. 함수를 호출할 때마다 다른 값을 반환 하기 때문에 템플릿의 다른 부분에서 허용 되지 않습니다. 동일한 매개 변수를 사용 하 여 동일한 템플릿에 배포 같은 결과 안정적으로 생성 하지 않습니다.

사용 하는 경우는 [이전 성공적인 배포를 다시 배포 하는 옵션](resource-group-template-deploy-rest.md#redeploy-when-deployment-fails), utcNow를 사용 하는 매개 변수를 포함 하는 이전 배포를 매개 변수 다시 평가 되지 않습니다. 대신 이전 배포에서 매개 변수 값을 롤백 배포에서 자동으로 재사용 됩니다.

UtcNow 함수에 대 한 기본값을 사용 하는 템플릿을 다시 배포 주의 해야 합니다. 다시 배포 하 고 매개 변수 값을 제공 하지는 다시 평가 됩니다. 새로 만들어야 하는 것이 아니라 기존 리소스를 업데이트 하려는 경우 이전 배포에서 매개 변수 값에 전달 합니다.

### <a name="return-value"></a>반환 값

현재 UTC 날짜/시간 값입니다.

### <a name="examples"></a>예

다음 예제에서는 서식 파일에는 날짜/시간 값에 대 한 다양 한 형식을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "utcValue": {
            "type": "string",
            "defaultValue": "[utcNow()]"
        },
        "utcShortValue": {
            "type": "string",
            "defaultValue": "[utcNow('d')]"
        },
        "utcCustomValue": {
            "type": "string",
            "defaultValue": "[utcNow('M d')]"
        }
    },
    "resources": [
    ],
    "outputs": {
        "utcOutput": {
            "type": "string",
            "value": "[parameters('utcValue')]"
        },
        "utcShortOutput": {
            "type": "string",
            "value": "[parameters('utcShortValue')]"
        },
        "utcCustomOutput": {
            "type": "string",
            "value": "[parameters('utcCustomValue')]"
        }
    }
}
```

출력 앞의 예제에서 각 배포에 대 한 다르지만 비슷합니다.

| 이름 | type | 값 |
| ---- | ---- | ----- |
| utcOutput | 문자열 | 20190305T175318Z |
| utcShortOutput | 문자열 | 03/05/2019 |
| utcCustomOutput | 문자열 | 3 5 |

다음 예제에서는 태그 값을 설정 하는 경우 함수에서 값을 사용 하는 방법을 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2018-05-01/subscriptionDeploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "utcShort": {
            "type": "string",
            "defaultValue": "[utcNow('d')]"
        },
        "rgName": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Resources/resourceGroups",
            "apiVersion": "2018-05-01",
            "name": "[parameters('rgName')]",
            "location": "westeurope",
            "tags":{
                "createdDate": "[parameters('utcShort')]"
            },
            "properties":{}
        }
    ],
    "outputs": {
        "utcShort": {
            "type": "string",
            "value": "[parameters('utcShort')]"
        }
    }
}
```

## <a name="next-steps"></a>다음 단계
* Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.
* 여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.
* 리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.
* 만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 애플리케이션 배포](resource-group-template-deploy.md)를 참조하세요.


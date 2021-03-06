---
title: 일관성 수준 및 Azure Cosmos DB API
description: Azure Cosmos DB에서 API에 대한 일관성 수준 이해
author: markjbrown
ms.author: mjbrown
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 10/23/2018
ms.reviewer: sngun
ms.openlocfilehash: b620ca76cfea296e504afffd91852308a01575db
ms.sourcegitcommit: e69fc381852ce8615ee318b5f77ae7c6123a744c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56002003"
---
# <a name="consistency-levels-and-azure-cosmos-db-apis"></a>일관성 수준 및 Azure Cosmos DB API

Azure Cosmos DB에서 제공되는 5가지 일관성 모델은 SQL API에서 기본적으로 지원됩니다. Azure Cosmos DB를 사용하는 경우 SQL API는 기본값입니다. 

Azure Cosmos DB는 인기 있는 데이터베이스에 대한 와이어 프로토콜 호환 API를 기본적으로 지원합니다. 데이터베이스에는 MongoDB, Apache Cassandra, Gremlin 및 Azure Table Storage가 있습니다. 이러한 데이터베이스는 정확하게 정의된 일관성 모델 또는 일관성 수준에 대한 SLA 지원 보장을 제공하지 않습니다. 이러한 데이터베이스는 일반적으로 Azure Cosmos DB에서 제공된 5가지 일관성 모델의 하위 집합만 제공합니다. SQL API, Gremlin API 및 Table API의 경우 Azure Cosmos 계정에서 구성된 기본 일관성 수준을 사용합니다. 

다음 섹션은 Apache Cassandra 및 MongoDB용 OSS 클라이언트 드라이버로 요청된 데이터 일관성 간의 매핑을 각각 보여주며, Azure Cosmos DB에서 해당 일관성 수준을 보여 줍니다.

## <a id="cassandra-mapping"></a>Apache Cassandra 및 Azure Cosmos DB 일관성 수준 간 매핑

아래 표는 Cassandra API에 사용할 수 있는 다양한 일관성 조합과 Cosmos DB의 동등한 기본 일관성 수준 매핑을 설명합니다. Apache Cassandra 쓰기 및 읽기 모드의 모든 조합은 Cosmos DB에서 기본적으로 지원됩니다. Apache Cassandra 쓰기 및 읽기 일관성 모델의 모든 조합에서 Cosmos DB는 Apache Cassandra와 동일하거나 더 높은 일관성 보장을 제공합니다. 또한 Cosmos DB는 가장 약한 쓰기 모드에서도 Apache Cassandra보다 높은 내구성을 제공합니다.

다음 표는 Azure Cosmos DB와 Cassandra 사이의 **쓰기 일관성 매핑**을 보여 줍니다.

| Cassandra | Azure Cosmos DB | 보증 |
| - | - | - |
|ALL|강력  | 선형화 가능성 |
| EACH_QUORUM   | 강력    | 선형화 가능성 | 
| QUORUM, SERIAL |  강력 |    선형화 가능성 |
| LOCAL_QUORUM, THREE, TWO, ONE, LOCAL_ONE, ANY | 일관적인 접두사 |전역적으로 일관적인 접두사 |
| EACH_QUORUM   | 강력    | 선형화 가능성 |
| QUORUM, SERIAL |  강력 |    선형화 가능성 |
| LOCAL_QUORUM, THREE, TWO, ONE, LOCAL_ONE, ANY | 일관적인 접두사 | 전역적으로 일관적인 접두사 |
| QUORUM, SERIAL | 강력   | 선형화 가능성 |
| LOCAL_QUORUM, THREE, TWO, ONE, LOCAL_ONE, ANY | 일관적인 접두사 | 전역적으로 일관적인 접두사 |
| LOCAL_QUORUM, LOCAL_SERIAL, TWO, THREE    | 제한된 부실 | <ul><li>제한된 부실입니다.</li><li>최대 K 버전 또는 t 시간만큼 뒤쳐져 있습니다.</li><li>해당 지역에서 최근에 커밋된 값을 읽습니다.</li></ul> |
| ONE, LOCAL_ONE, ANY   | 일관적인 접두사 | 하위 지역 일관적인 접두사 |

다음 표는 Azure Cosmos DB와 Cassandra 사이의 **읽기 일관성 매핑**을 보여 줍니다.

| Cassandra | Azure Cosmos DB | 보증 |
| - | - | - |
| ALL, QUORUM, SERIAL, LOCAL_QUORUM, LOCAL_SERIAL, THREE, TWO, ONE, LOCAL_ONE | 강력  | 선형화 가능성|
| ALL, QUORUM, SERIAL, LOCAL_QUORUM, LOCAL_SERIAL, THREE, TWO   |강력 |   선형화 가능성 |
|LOCAL_ONE, ONE | 일관적인 접두사 | 전역적으로 일관적인 접두사 |
| ALL, QUORUM, SERIAL   | 강력    | 선형화 가능성 |
| LOCAL_ONE, ONE, LOCAL_QUORUM, LOCAL_SERIAL, TWO, THREE |  일관적인 접두사   | 전역적으로 일관적인 접두사 |
| LOCAL_ONE, ONE, TWO, THREE, LOCAL_QUORUM, QUORUM |    일관적인 접두사   | 전역적으로 일관적인 접두사 |
| ALL, QUORUM, SERIAL, LOCAL_QUORUM, LOCAL_SERIAL, THREE, TWO   |강력 |   선형화 가능성 |
| LOCAL_ONE, ONE    | 일관적인 접두사 | 전역적으로 일관적인 접두사|
| ALL, QUORUM, SERIAL   Strong  Linearizability
LOCAL_ONE, ONE, LOCAL_QUORUM, LOCAL_SERIAL, TWO, THREE  |일관적인 접두사  | 전역적으로 일관적인 접두사 |
|ALL    |강력 |선형화 가능성 |
| LOCAL_ONE, ONE, TWO, THREE, LOCAL_QUORUM, QUORUM  |일관적인 접두사  |전역적으로 일관적인 접두사|
|ALL, QUORUM, SERIAL Strong Linearizability
LOCAL_ONE, ONE, LOCAL_QUORUM, LOCAL_SERIAL, TWO, THREE  |일관적인 접두사  |전역적으로 일관적인 접두사 |
|ALL    |강력 | 선형화 가능성 |
| LOCAL_ONE, ONE, TWO, THREE, LOCAL_QUORUM, QUORUM  | 일관적인 접두사 | 전역적으로 일관적인 접두사 |
| QUORUM, LOCAL_QUORUM, LOCAL_SERIAL, TWO, THREE |  제한된 부실   | <ul><li>제한된 부실입니다.</li><li>최대 K 버전 또는 t 시간만큼 뒤쳐져 있습니다. </li><li>해당 지역에서 최근에 커밋된 값을 읽습니다.</li></ul>
| LOCAL_ONE, ONE |일관적인 접두사 | 하위 지역 일관적인 접두사 |
| LOCAL_ONE, ONE, TWO, THREE, LOCAL_QUORUM, QUORUM  | 일관적인 접두사 | 하위 지역 일관적인 접두사 |


## <a id="mongo-mapping"></a>MongoDB 3.4 및 Azure Cosmos DB 일관성 수준 간의 매핑

다음 테이블에서는 MongoDB 3.4와 Azure Cosmos DB의 기본 일관성 수준 간의 “읽기 문제” 매핑을 보여줍니다. 또한 다중 지역 및 단일 지역 배포도 보여 줍니다.

| **MongoDB 3.4** | **Azure Cosmos DB(다중 영역)** | **Azure Cosmos DB(단일 영역)** |
| - | - | - |
| 선형화 가능 | 강력 | 강력 |
| 과반수 | 제한된 부실 | 강력 |
| Local | 일관적인 접두사 | 일관적인 접두사 |

## <a name="next-steps"></a>다음 단계

오픈 소스 API 및 Cosmos DB API 간의 일관성 수준 및 호환성에 대해 자세히 알아봅니다. 다음 문서를 참조하세요.

* [다양한 일관성 수준의 가용성 및 성능 절충](consistency-levels-tradeoffs.md)
* [Azure Cosmos DB의 API for MongoDB에서 지원되는 MongoDB 기능](mongodb-feature-support.md)
* [Azure Cosmos DB Cassandra API에서 지원된 Apache Cassandra 기능](cassandra-support.md)
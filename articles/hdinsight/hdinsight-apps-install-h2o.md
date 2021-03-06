---
title: 게시된 애플리케이션 설치 - H2O Sparkling Water - Azure HDInsight
description: 타사의 Hadoop 애플리케이션 H2O Sparkling Water를 설치하여 사용합니다.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: ashish
ms.openlocfilehash: 4be346163fd54c0c5f962d15bc2433c7fab49e0b
ms.sourcegitcommit: e68df5b9c04b11c8f24d616f4e687fe4e773253c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53650946"
---
# <a name="install-published-application---h2o-sparkling-water"></a>게시된 애플리케이션 설치 - H2O Sparkling Water

이 문서에서는 [H20 Sparkling Water](https://www.h2o.ai/)에 게시된 [Apache Hadoop](https://hadoop.apache.org/) 애플리케이션을 Azure HDInsight에 설치하고 실행하는 방법을 설명합니다. HDInsight 애플리케이션 플랫폼 개요 및 사용 가능한 ISV(Independent Software Vendor) 게시된 애플리케이션 목록은 [타사 Hadoop 애플리케이션 설치](hdinsight-apps-install-applications.md)를 참조하세요. 사용자 고유의 애플리케이션을 설치하는 방법에 대한 지침은 [사용자 지정 HDInsight 애플리케이션 설치](hdinsight-apps-install-custom-applications.md)를 참조하세요.

## <a name="about-h2o-sparkling-water"></a>H2O Sparkling Water 정보

H2O Sparkling Water는 선형 확장성을 갖춘 완벽하게 분산된 오픈 소스 메모리 내 기계 학습 플랫폼입니다. H2O Sparkling Water를 사용하여 H2O의 빠르고 확장성 있는 기계 학습 알고리즘을 [Apache Spark](https://spark.apache.org/) 기능과 결합할 수 있습니다. Sparkling Water가 있으면 H2O Flow UI를 사용하여 [Scala](https://www.scala-lang.org/), R 및 Python에서 계산을 유도할 수 있습니다.

다음은 H2O Sparkling Water의 특징입니다.

* **사용하기 쉬운 WebUI 및 친숙한 인터페이스** - H2O의 직관적인 웹 기반 Flow GUI 또는 R, Python, Java, Scala, JSON, H2O API 등과 같은 프로그래밍 환경을 사용하여 신속하게 설치하고 시작할 수 있습니다.
* **모든 일반 데이터베이스 및 파일 형식에 대한 데이터 진단 지원** – Microsoft Excel, R Studio, Tableau 내에서 빅 데이터를 간편하게 탐색하고 모델링할 수 있습니다. HDFS, S3, SQL 및 NoSQL 데이터 원본에서 데이터에 연결합니다.
* **확장성이 매우 뛰어난 빅 데이터 마이닝 및 분석** – H2O Big Joins는 R data.table 작업보다 7배 빠르게 수행할 수 있으며, 100억 x 100억 행 조인으로 선형 확장이 가능합니다.
* **실시간 데이터 점수 매기기** – POJO(plain-old Java objects), MOJO(model-optimized Java objects) 또는 H2O REST API를 사용하여 모델을 프로덕션 환경에 신속하게 배포할 수 있습니다.

### <a name="resource-links"></a>리소스 링크

* [H2O.ai 엔지니어링 로드맵](http://jira.h2o.ai/)
* [H2O.ai 홈](https://www.h2o.ai/)
* [H2O.ai 설명서](http://docs.h2o.ai/)
* [H2O.ai 지원](https://support.h2o.ai/)
* [H2O.ai 오픈 소스 코드베이스](https://github.com/h2oai/)

## <a name="prerequisites"></a>필수 조건

새 HDInsight 클러스터 또는 기존 클러스터에 이 앱을 설치하려면 다음 구성이 필요합니다.

* 클러스터 계층: Standard 또는 Premium
* 클러스터 유형: Spark
* 클러스터 버전: 3.5 또는 3.6

## <a name="install-the-h2o-sparkling-water-published-application"></a>H2O Sparkling Water 게시된 애플리케이션 설치

이 애플리케이션 및 사용 가능한 다른 ISV 애플리케이션을 설치하는 단계별 지침은 [타사 Apache Hadoop 애플리케이션 설치](hdinsight-apps-install-applications.md)를 참조하세요.

## <a name="launch-h2o-sparkling-water"></a>H2O Sparkling Water 실행

1. 설치가 끝나면 [Jupyter Notebooks](https://jupyter.org/)(`https://<ClusterName>.azurehdinsight.net/jupyter`)을 열고 Azure Portal의 클러스터에서 H2O Sparkling Water(h2o-sparklingwater)를 사용할 수 있습니다. 포털의 클러스터 창에서 **클러스터 대시보드**를 선택한 다음, **Jupyter Notebook**을 선택하여 Jupyter에 액세스할 수도 있습니다. 자격 증명을 입력하라는 메시지가 표시됩니다. 클러스터를 만들 때 지정한 클러스터의 Hadoop 자격 증명을 입력합니다.

2. Jupyter에 H2O-PySparkling-Examples, PySpark Examples 및 Scala Examples의 3개 폴더가 있습니다. **H2O-PySparkling-Examples** 폴더를 선택합니다.

    ![Jupyter Notebook 홈](./media/hdinsight-apps-install-h2o/jupyter-home.png)

3. 새 Notebook을 만드는 첫 번째 단계는 Spark 환경을 구성하는 것입니다. 이 정보는 **Sentiment_analysis_with_Sparkling_Water** 예제에 포함되어 있습니다. Spark 환경을 구성할 때 올바른 jar를 사용하고, 첫 번째 셀의 출력에서 제공하는 IP 주소를 지정해야 합니다.

    ![Jupyter Notebook 홈](./media/hdinsight-apps-install-h2o/spark-config.png)

4. H2O 클러스터를 시작합니다.

    ![클러스터 시작](./media/hdinsight-apps-install-h2o/start-cluster.png)

5. H2O 클러스터를 실행한 후에는**`https://<ClusterName>-h2o.apps.azurehdinsight.net:443`** 으로 이동하여 H2O Flow를 엽니다.

    > [!NOTE]  
    > H2O Flow를 열 수 없는 경우 브라우저 캐시를 지워봅니다. 그래도 열 수 없는 경우 클러스터의 리소스가 충분하지 않은 것입니다. 클러스터 창의 **클러스터 크기 조정** 아래에서 작업자 노드 수를 늘려보세요.

    ![H2O Flow 대시보드](./media/hdinsight-apps-install-h2o/h2o-flow.png)

6. 오른쪽에 있는 메뉴에서 **Million_Songs.flow** 예제를 선택합니다. 경고와 함께 대화 상자가 나타나면 **Notebook 로드**를 클릭합니다. 이 데모는 실제 데이터를 사용하여 몇 분 후에 실행되도록 설계되었습니다. 이진 분류를 사용하여 노래가 2004년 전에 발표되었는지 아니면 후에 발표되었는지 데이터를 통해 예측하는 것이 목표입니다.

    ![Million_Songs.flow 선택](./media/hdinsight-apps-install-h2o/million-songs.png)

7. **milsongs-cls-train.csv.gz**를 포함하는 경로를 찾고 전체 경로를 **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-train.csv.gz**로 바꿉니다.

8. **milsongs-cls-test.csv.gz**를 포함하는 경로를 찾고 이 경로를 **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-test.csv.gz**로 바꿉니다.

9. Notebook 셀에 있는 모든 명령문을 실행하려면 도구 모음에서 **모두 실행** 단추를 선택합니다.

    ![모두 실행](./media/hdinsight-apps-install-h2o/run-all.png)

10. 몇 분 후, 다음과 유사한 결과가 표시됩니다.

    ![출력](./media/hdinsight-apps-install-h2o/output.png)

이것으로 끝입니다. Spark에서 몇 분 동안 인공 지능을 활용하셨습니다. 이제 H2O Flow에서 다양한 유형의 기계 학습 알고리즘을 보여 주는 더 많은 예제를 살펴볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

* [H2O 설명서](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/index.html)
* [사용자 지정 HDInsight 애플리케이션 설치](hdinsight-apps-install-custom-applications.md): 게시 취소된 HDInsight 애플리케이션을 HDInsight에 배포하는 방법을 알아봅니다.
* [HDInsight 애플리케이션 게시](hdinsight-apps-publish-applications.md): 사용자 지정 HDInsight 애플리케이션을 Azure Marketplace에 게시하는 방법을 알아봅니다.
* [MSDN: HDInsight 애플리케이션 설치](https://msdn.microsoft.com/library/mt706515.aspx): HDInsight 애플리케이션을 정의하는 방법을 알아봅니다.
* [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 스크립트 작업을 사용하여 추가 애플리케이션을 설치하는 방법을 알아봅니다.
* [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md): 빈 에지 노드를 사용하여 HDInsight 클러스터에 액세스하고 HDInsight 애플리케이션을 테스트 및 호스팅하는 방법을 알아봅니다.

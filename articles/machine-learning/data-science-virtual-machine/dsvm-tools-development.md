---
title: 데이터 과학 Virtual Machine 개발 도구 - Azure | Microsoft Docs
description: Data Science Virtual Machine에 사전 설치된 도구 및 통합 개발 환경에 대해 알아봅니다.
keywords: 데이터 과학 도구, 데이터 과학 가상 머신, 데이터 과학용 도구, linux 데이터 과학
services: machine-learning
documentationcenter: ''
author: gopitk
manager: cgronlun
ms.custom: seodec18
ms.assetid: ''
ms.service: machine-learning
ms.subservice: data-science-vm
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2017
ms.author: gokuma
ms.openlocfilehash: 7983169c2b1123c57a48471e3f4d9ad6f19c84dc
ms.sourcegitcommit: 90dcc3d427af1264d6ac2b9bde6cdad364ceefcc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2019
ms.locfileid: "58314725"
---
# <a name="development-tools-on-the-data-science-virtual-machine"></a>데이터 과학 Virtual Machine의 개발 도구

DSVM(데이터 과학 Virtual Machine)은 많이 사용되는 여러 도구와 IDE를 묶음으로 개발을 위한 생산적인 환경을 제공합니다. DSVM에서 제공되는 몇 가지 도구는 다음과 같습니다. 

## <a name="visual-studio-2017"></a>Visual Studio 2017  

|    |           |
| ------------- | ------------- |
| 무엇인가요?   | 범용 IDE      |
| 지원되는 DSVM 버전      | Windows      |
| 일반적인 사용 용도      | 소프트웨어 개발    |
| DSVM에 구성/설치 방법      | 데이터 과학 워크로드(Python 및 R 도구), Azure 워크로드(Hadoop, Data Lake), Node.js, SQL Server 도구, [Azure Machine Learning for Visual Studio Code](https://github.com/Microsoft/vs-tools-for-ai)    |
| 사용/실행 방법      | 바탕 화면 바로 가기(`C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv.exe`)    |
| DSVM의 관련 도구      |     Visual Studio Code, RStudio, Juno  |

## <a name="visual-studio-code"></a>Visual Studio Code 

|    |           |
| ------------- | ------------- |
| 무엇인가요?   | 범용 IDE      |
| 지원되는 DSVM 버전      | Windows, Linux     |
| 일반적인 사용 용도      | 코드 편집기 및 Git 통합   |
| 사용/실행 방법      | Windows의 바탕 화면 바로 가기(`C:\Program Files (x86)\Microsoft VS Code\Code.exe`), Linux의 바탕 화면 바로 가기 또는 터미널(`code`)    |
| DSVM의 관련 도구      |     Visual Studio 2017, RStudio, Juno  |

## <a name="rstudio--desktop"></a>RStudio Desktop 

|    |           |
| ------------- | ------------- |
| 무엇인가요?   | R용 클라이언트 IDE    |
| 지원되는 DSVM 버전      | Windows, Linux      |
| 일반적인 사용 용도      |  R 개발     |
| 사용/실행 방법      | Windows에서 바탕 화면 바로 가기(`C:\Program Files\RStudio\bin\rstudio.exe`), Linux에서 바탕 화면 바로 가기(`/usr/bin/rstudio`)      |
| DSVM의 관련 도구      |   Visual Studio 2017, Visual Studio Code, Juno      |

## <a name="rstudio--server"></a>RStudio  Server 

|    |           |
| ------------- | ------------- |
| 무엇인가요?   | R용 웹 기반 IDE    |
| 지원되는 DSVM 버전      | Linux      |
| 일반적인 사용 용도      |  R 개발     |
| 사용/실행 방법      | _systemctl enable rstudio-server_를 사용하여 서비스를 사용하도록 설정한 다음, _systemctl start rstudio-server_로 서비스를 시작합니다. 로그인 할 수 있습니다 다음 RStudio Server에 http:\//-vm-ip:8787 합니다.       |
| DSVM의 관련 도구      |   Visual Studio 2017, Visual Studio Code, RStudio Desktop      |

## <a name="juno"></a>Juno 

|    |           |
| ------------- | ------------- |
| 무엇인가요?   | Julia 언어용 클라이언트 IDE   |
| 지원되는 DSVM 버전      | Windows, Linux      |
| 일반적인 사용 용도      |  Julia 개발     |
| 사용/실행 방법      | Windows에서 바탕 화면 바로 가기(`C:\JuliaPro-0.5.1.1\Juno.bat`), Linux에서 바탕 화면 바로 가기(`/opt/JuliaPro-VERSION/Juno`)      |
| DSVM의 관련 도구      |   Visual Studio 2017, Visual Studio Code, RStudio      |

## <a name="pycharm"></a>Pycharm

|    |           |
| ------------- | ------------- |
| 무엇인가요?   | Python 언어용 클라이언트 IDE    |
| 지원되는 DSVM 버전      | Linux      |
| 일반적인 사용 용도      |  Python 개발     |
| 사용/실행 방법      | Linux에서 바탕 화면 바로 가기(`/usr/bin/pycharm`)      |
| DSVM의 관련 도구      |   Visual Studio 2017, Visual Studio Code, RStudio      |



## <a name="powerbi-desktop"></a>PowerBI Desktop 

|    |           |
| ------------- | ------------- |
| 무엇인가요?   | 대화형 데이터 시각화 및 BI 도구    |
| 지원되는 DSVM 버전      | Windows  |
| 일반적인 사용 용도      |  데이터 시각화 및 대시보드 작성   |
| 사용/실행 방법      | 바탕 화면 바로 가기(`C:\Program Files\Microsoft Power BI Desktop\bin\PBIDesktop.exe`)      |
| DSVM의 관련 도구      |   Visual Studio 2017, Visual Studio Code, Juno      |


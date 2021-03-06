---
title: AzCopy v10(미리 보기)을 사용하여 Azure Storage로 데이터 복사 또는 이동 | Microsoft Docs
description: AzCopy v10(미리 보기) 유틸리티를 사용하여 Blob, 데이터 레이크 및 파일 콘텐츠 간에 데이터를 이동하거나 복사합니다. 로컬 파일에서 Azure Storage로 데이터를 복사하거나, Storage 계정 내에서 데이터를 복사하거나, Storage 계정 간에 데이터를 복사합니다. 데이터를 Azure Storage로 손쉽게 마이그레이션할 수 있습니다.
services: storage
author: artemuwka
ms.service: storage
ms.topic: article
ms.date: 02/24/2019
ms.author: artemuwka
ms.subservice: common
ms.openlocfilehash: 111c24c1cd608542a5ef7da85f93ca22082af6d9
ms.sourcegitcommit: 235cd1c4f003a7f8459b9761a623f000dd9e50ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/11/2019
ms.locfileid: "57726722"
---
# <a name="transfer-data-with-the-azcopy-v10-preview"></a>AzCopy v10(미리 보기)을 사용하여 데이터 전송

AzCopy v10(미리 보기)은 Microsoft Azure Blob 및 File Storage와 데이터를 복사하는 데 사용되는 차세대 명령줄 유틸리티로, 안정적인 고성능 데이터 전송을 위해 다시 디자인된 명령줄 인터페이스와 새 아키텍처를 제공합니다. AzCopy를 사용하여 파일 시스템과 저장소 계정 간 또는 저장소 계정 간에 데이터를 복사할 수 있습니다.

## <a name="whats-new-in-azcopy-v10"></a>AzCopy v10의 새로운 기능

- 파일 시스템을 Azure Blob에 또는 그 반대로 동기화합니다. `azcopy sync <source> <destination>`를 사용합니다. 증분 복사 시나리오에 적합합니다.
- Azure Data Lake Storage Gen2 API를 지원합니다. ADLS Gen2 API를 호출하는 URI로 `myaccount.dfs.core.windows.net`을 사용하세요.
- 계정 전체를 다른 계정으로 복사하는 기능을 지원합니다(Blob 서비스만 해당).
- 계정은 계정 복사할 새 사용 이제 [URL에서 블록 배치](https://docs.microsoft.com/rest/api/storageservices/put-block-from-url) Api. 클라이언트에 데이터를 전송할 필요가 없기 때문에 더 빠르게 전송할 수 있습니다.
- 지정된 경로의 파일 및 BLOB을 나열/제거합니다.
- 플래그를 제외 하는 에서처럼-도 경로에 와일드 카드 패턴을 지원 합니다.
- 향상된 복원력: 모든 AzCopy 인스턴스는 작업 순서 및 관련 로그 파일을 만듭니다. 이전 작업을 살펴보고 다시 시작하고, 실패한 작업을 재개할 수 있습니다. AzCopy는 전송 실패 후 자동으로 전송을 다시 시도합니다.
- 일반적인 성능이 향상되었습니다.

## <a name="download-and-install-azcopy"></a>AzCopy 다운로드 및 설치

### <a name="latest-preview-version-v10"></a>최신 미리 보기 버전(v10)

AzCopy의 최신 미리 보기 버전을 다운로드합니다.
- [Windows](https://aka.ms/downloadazcopy-v10-windows) (zip)
- [Linux](https://aka.ms/downloadazcopy-v10-linux) (tar)
- [MacOS](https://aka.ms/downloadazcopy-v10-mac) (zip)

### <a name="latest-production-version-v81"></a>최신 프로덕션 버전(v8.1)

[Windows용 AzCopy의 최신 프로덕션 버전](https://aka.ms/downloadazcopy)을 다운로드합니다.

### <a name="azcopy-supporting-table-storage-service-v73"></a>Table Storage 서비스(v7.3)를 지원하는 AzCopy

[Microsoft Azure Table Storage 서비스와 데이터 복사를 지원하는 AzCopy v7.3](https://aka.ms/downloadazcopynet)을 다운로드합니다.

## <a name="post-installation-steps"></a>설치 후 단계

AzCopy v10은 설치가 필요하지 않습니다. 기본 명령줄 응용 프로그램을 열고 폴더를 이동할 위치 `azcopy.exe` (Windows) 또는 `azcopy` (Linux) 실행 파일이 있습니다. 원하는 경우 시스템 경로에 AzCopy 폴더 위치를 추가할 수 있습니다.

## <a name="authentication-options"></a>인증 옵션

AzCopy v10을 사용하면 Azure Storage로 인증할 때 다음 옵션을 사용할 수 있습니다.
- **Azure Active Directory[Blob 및 ADLS Gen2 서비스 지원]**. Azure Active Directory를 사용하여 ```.\azcopy login```으로 로그인합니다.  사용자가 Azure Active Directory 인증을 사용하여 Blob 스토리지에 데이터를 쓰려면 ["Storage Blob 데이터 기여자" 역할이 할당](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac)되어야 합니다. Managed Service Identity (MSI)를 사용 하 여 인증을 사용 하 여 `azcopy login --identity` 후 Azure 계산 인스턴스 데이터 참가자 역할을 부여 합니다.
- **SAS 토큰[Blob 및 파일 서비스 지원]**. 명령줄에서 Blob 경로에 SAS 토큰을 추가하여 사용합니다. Azure Portal, [Storage 탐색기](https://blogs.msdn.microsoft.com/jpsanders/2017/10/12/easily-create-a-sas-to-download-a-file-from-azure-storage-using-azure-storage-explorer/), [PowerShell](https://docs.microsoft.com/powershell/module/az.storage/new-azstorageblobsastoken) 또는 원하는 다른 도구를 사용하여 SAS 토큰을 생성할 수 있습니다. 자세한 내용은 [예제](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2)를 참조하세요.

## <a name="getting-started"></a>시작

> [!TIP]
> **그래픽 사용자 인터페이스를 선호 하십니까?**
>
> 시도 [Azure Storage 탐색기](https://azure.microsoft.com/features/storage-explorer/), Azure Storage 데이터 관리를 간소화 하는 데스크톱 클라이언트 및 **AzCopy를 사용 하 여 이제** 데이터 전송에 Azure storage를 가속화 하 합니다.
>
> 간단히 '미리 보기' 메뉴 아래에서 Storage 탐색기에서 AzCopy 기능을 사용 하도록 설정 합니다. Storage 탐색기의 업로드 및 성능 향상된을 위해 Blob 저장소로 데이터를 다운로드 하는 경우 AzCopy 사용 합니다.
> ![Azure Storage 탐색기에서 전송 엔진으로 AzCopy를 사용 하도록 설정](media/storage-use-azcopy-v10/enable-azcopy-storage-explorer.jpg)

AzCopy v10은 간단한 자체 문서화 구문을 갖고 있습니다. Azure Active Directory에 로그인한 경우 일반 구문은 다음과 같이 표시됩니다.

```azcopy
.\azcopy <command> <arguments> --<flag-name>=<flag-value>
# Examples if you have logged into the Azure Active Directory:
.\azcopy copy <source path> <destination path> --<flag-name>=<flag-value>
.\azcopy cp "C:\local\path" "https://account.blob.core.windows.net/container" --recursive=true
.\azcopy cp "C:\local\path\myfile" "https://account.blob.core.windows.net/container/myfile"
.\azcopy cp "C:\local\path\*" "https://account.blob.core.windows.net/container"

# Examples if you are using SAS tokens to authenticate:
.\azcopy cp "C:\local\path" "https://account.blob.core.windows.net/container?sastoken" --recursive=true
.\azcopy cp "C:\local\path\myfile" "https://account.blob.core.windows.net/container/myfile?sastoken"
```

다음과 같은 방법으로 사용 가능한 명령 목록을 가져올 수 있습니다.

```azcopy
.\azcopy --help
# Using the alias instead
.\azcopy -h
```

특정 명령에 대한 도움말 페이지 및 예제를 보려면 아래 명령을 실행합니다.

```azcopy
.\azcopy <cmd> --help
# Example:
.\azcopy cp -h
```

## <a name="create-a-blob-container-or-file-share"></a>Blob 컨테이너 또는 파일 공유 만들기 

**Blob 컨테이너 만들기**

```azcopy
.\azcopy make "https://account.blob.core.windows.net/container-name"
```

**파일 공유 만들기**

```azcopy
.\azcopy make "https://account.file.core.windows.net/share-name"
```

**ADLS Gen2를 사용하여 Blob 컨테이너 만들기**

Blob 스토리지 계정에서 계층 구조 네임스페이스를 사용하도록 설정한 경우 다음 명령을 사용하여 파일을 업로드할 수 있도록 새 파일 시스템(Blob 컨테이너)을 만들 수 있습니다.

```azcopy
.\azcopy make "https://account.dfs.core.windows.net/top-level-resource-name"
```

## <a name="copy-data-to-azure-storage"></a>Azure Storage에 데이터 복사

복사 명령을 사용하여 원본에서 대상으로 데이터를 전송합니다. 원본/대상으로 사용 가능한 항목은 다음과 같습니다.
- 로컬 파일 시스템
- Azure Blob/가상 디렉터리/컨테이너 URI
- Azure 파일/디렉터리/파일 공유 URI
- Azure Data Lake Storage Gen2 파일 시스템/디렉터리/파일 URI

```azcopy
.\azcopy copy <source path> <destination path> --<flag-name>=<flag-value>
# Using alias instead
.\azcopy cp <source path> <destination path> --<flag-name>=<flag-value>
```

다음 명령은 `C:\local\path` 폴더의 모든 파일을 `mycontainer1` 컨테이너에 재귀적으로 업로드하고 해당 컨테이너에서 `path` 디렉터리를 만듭니다.

```azcopy
.\azcopy cp "C:\local\path" "https://account.blob.core.windows.net/mycontainer1<sastoken>" --recursive=true
```

다음 명령은 `C:\local\path` 폴더의 모든 파일을 `mycontainer1` 컨테이너에 업로드합니다(하위 디렉터리로 반복하지 않고).

```azcopy
.\azcopy cp "C:\local\path\*" "https://account.blob.core.windows.net/mycontainer1<sastoken>"
```

예제를 더 가져오려면 다음 명령을 사용합니다.

```azcopy
.\azcopy cp -h
```

## <a name="copy-data-between-two-storage-accounts"></a>두 저장소 계정 간에 데이터 복사

두 저장소 계정 간에 데이터를 복사할 때에는 [Put Block From URL](https://docs.microsoft.com/rest/api/storageservices/put-block-from-url) API를 사용하고 클라이언트 머신의 네트워크 대역폭을 사용하지 않습니다. 두 Azure Storage 서버 간에 데이터가 직접 복사되고, AzCopy는 단순히 복사 작업을 오케스트레이션합니다. 이 옵션은 현재 Blob 스토리지에만 사용할 수 있습니다.

두 저장소 계정 간에 데이터를 복사하려면 다음 명령을 사용합니다.
```azcopy
.\azcopy cp "https://account.blob.core.windows.net/<sastoken>" "https://otheraccount.blob.core.windows.net/<sastoken>" --recursive=true
```

> [!NOTE]
> 이 명령은 모든 Blob 컨테이너를 열거하고 대상 계정에 복사합니다. 현재 AzCopy v10은 두 저장소 계정 간의 블록 Blob 복사만 지원합니다. 그 외의 모든 저장소 계정 개체(추가 Blob, 페이지 Blob, 파일, 테이블 및 큐)를 건너뜁니다.

## <a name="copy-a-vhd-image-to-a-storage-account"></a>VHD 이미지를 저장소 계정에 복사

사용 하 여 `--blob-type=PageBlob` 디스크 이미지를 페이지 Blob으로 Blob storage에 업로드 합니다.

```azcopy
.\azcopy cp "C:\myimages\diskimage.vhd" "https://account.blob.core.windows.net/mycontainer/diskimage.vhd<sastoken>" --blob-type=PageBlob
```

## <a name="sync-incremental-copy-and-optional-delete-blob-storage-only"></a>동기화: 증분 복사 및 (선택 사항) 삭제 (Blob storage에만 해당)

동기화 명령은 디렉터리에 대상 비교 하는 파일 이름 및 마지막 수정된 타임 스탬프를 원본 디렉터리의 콘텐츠를 동기화합니다. 원본에 존재 하지 않는 경우이 작업에서 대상 파일의 삭제를 포함 하는 필요에 따라 때 `--delete-destination=prompt|true` 플래그에서 제공 됩니다. 기본적으로 delete 동작을 사용 하는 사용할 수 없습니다.

> [!NOTE]
> 사용 하 여 `--delete-destination` 주의 해 서 플래그입니다. 사용 하도록 설정 [일시 삭제](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete) 삭제 동작 계정의 실수로 인 한 삭제를 방지 하려면 동기화를 활성화 하기 전에 기능입니다.
>
> 때 `--delete-destination` 로 설정 된 true, AzCopy는 파일을 삭제 사용자에 게 프롬프트 없이 대상에서 원본에 존재 하지 않습니다. 확인 메시지가 표시 된다는 하려는 경우 사용 하 여 `--delete-destination=prompt`입니다.

로컬 파일 시스템을 저장소 계정과 동기화하려면 다음 명령을 사용합니다.

```azcopy
.\azcopy sync "C:\local\path" "https://account.blob.core.windows.net/mycontainer<sastoken>"
```

같은 방법으로 Blob 컨테이너를 로컬 파일 시스템과 동기화할 수 있습니다.

```azcopy
# If you're using Azure Active Directory authentication the sastoken is not required
.\azcopy sync "https://account.blob.core.windows.net/mycontainer" "C:\local\path"
```

이 명령을 사용하면 마지막으로 수정된 타임스탬프에 따라 원본을 대상과 증분 방식으로 동기화할 수 있습니다. 원본에서 파일이 추가 또는 삭제되면 AzCopy v10이 대상에서 똑같은 작업을 수행합니다. 삭제 동작 동기화 명령에서 사용 하는 경우 AzCopy에서에서 삭제 됩니다 파일을 대상이 존재 하지 않는 원본에서 더 이상 하는 경우.

## <a name="advanced-configuration"></a>고급 구성

### <a name="configure-proxy-settings"></a>프록시 설정 구성

AzCopy v10에 대한 프록시 설정을 구성하려면 다음 명령을 사용하여 환경 변수 https_proxy를 설정합니다.

```cmd
# For Windows:
set https_proxy=<proxy IP>:<proxy port>
# For Linux:
export https_proxy=<proxy IP>:<proxy port>
# For MacOS
export https_proxy=<proxy IP>:<proxy port>
```

### <a name="optimize-throughput"></a>처리량 최적화

AZCOPY_CONCURRENCY_VALUE 환경 변수를 설정하여 동시 요청 수를 구성하고 처리량 성능 및 리소스 사용량을 제어할 수 있습니다. 이 값은 기본적으로 300으로 설정됩니다. 값을 줄이면 AzCopy v10에서 사용하는 대역폭 및 CPU가 제한됩니다.

```cmd
# For Windows:
set AZCOPY_CONCURRENCY_VALUE=<value>
# For Linux:
export AZCOPY_CONCURRENCY_VALUE=<value>
# For MacOS
export AZCOPY_CONCURRENCY_VALUE=<value>
# To check the current value of the variable on all the platforms
.\azcopy env
# If the value is blank then the default value is currently in use
```

### <a name="change-the-location-of-the-log-files"></a>로그 파일의 위치 변경

필요에 따라 또는 OS 디스크가 채워지는 것을 방지하기 위해 로그 파일의 위치를 변경할 수 있습니다.

```cmd
# For Windows:
set AZCOPY_LOG_LOCATION=<value>
# For Linux:
export AZCOPY_LOG_LOCATION=<value>
# For MacOS
export AZCOPY_LOG_LOCATION=<value>
# To check the current value of the variable on all the platforms
.\azcopy env
# If the value is blank then the default value is currently in use
```

### <a name="change-the-default-log-level"></a>기본 로그 수준 변경

기본적으로 AzCopy 로그 수준은 INFO로 설정됩니다. 디스크 공간 절약을 위해 로그의 세부 정보 표시를 줄이려는 경우 ``--log-level`` 옵션을 사용하여 설정을 덮어씁니다. 사용 가능한 로그 수준은 다음과 같습니다. DEBUG, INFO, WARNING, ERROR, PANIC 및 FATAL

## <a name="troubleshooting"></a>문제 해결

AzCopy v10은 모든 작업에 대한 로그 파일 및 계획 파일을 만듭니다. 로그를 사용하여 잠재적 문제를 조사하고 해결할 수 있습니다. 로그에는 실패 상태(UPLOADFAILED, COPYFAILED 및 DOWNLOADFAILED), 전체 경로, 실패 이유가 포함됩니다. 작업 로그 및 계획 파일 % USERPROFILE %에 위치한\\Windows 또는 $HOME.azcopy 폴더\\Mac 및 Linux에서.azcopy 폴더입니다.

> [!IMPORTANT]
> Microsoft 지원에 지원 요청을 제출하는 경우(또는 타사와 관련된 문제를 해결하려는 경우) SAS를 실수로 다른 사람과 공유하지 않도록 실행하려는 명령의 수정 버전을 공유해 주세요. 수정 버전은 로그 파일의 시작 부분에서 찾을 수 있습니다.

### <a name="review-the-logs-for-errors"></a>오류에 대한 로그 검토

다음 명령은 04dc9ca9-158f-7945-5933-564021086c79 로그에서 상태가 UPLOADFAILED인 모든 오류를 가져옵니다.

```azcopy
cat 04dc9ca9-158f-7945-5933-564021086c79.log | grep -i UPLOADFAILED
```

또는 사용 하 여 전송에 실패 한 파일 이름을 볼 수 있습니다 `azcopy jobs show <jobid> --with-status=Failed` 명령입니다.

### <a name="view-and-resume-jobs"></a>작업 보기 및 다시 시작

각 전송 작업은 AzCopy 작업을 만듭니다. 다음 명령을 사용하여 작업 기록을 볼 수 있습니다.

```azcopy
.\azcopy jobs list
```

작업 상태를 보려면 다음 명령을 사용합니다.

```azcopy
.\azcopy jobs show <job-id>
```

전송을 상태별로 필터링하려면 다음 명령을 사용합니다.

```azcopy
.\azcopy jobs show <job-id> --with-status=Failed
```

SAS 토큰(보안상의 이유로 지속되지 않음)과 함께 해당 식별자를 사용하여 실패/취소된 작업을 다시 시작할 수 있습니다.

```azcopy
.\azcopy jobs resume <jobid> --sourcesastokenhere --destinationsastokenhere
```

## <a name="next-steps"></a>다음 단계

피드백은 언제든지 환영합니다. 질문, 문제 또는 일반 피드백은 https://github.com/Azure/azure-storage-azcopy에서 제출하시면 됩니다. 감사합니다.

---
title: Azure에서 Recovery Services 자격 증명 모음 삭제
description: Recovery Services 자격 증명 모음을 삭제 하는 방법을 설명 합니다.
services: backup
author: rayne-wiselman
manager: carmonm
ms.service: backup
ms.topic: conceptual
ms.date: 03/05/2019
ms.author: raynew
ms.openlocfilehash: e83698af6bb1caab1568375b726753d34a8c8467
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "57861352"
---
# <a name="delete-a-recovery-services-vault"></a>Recovery Services 자격 증명 모음 삭제

이 문서에서는 삭제 하는 방법에 설명 합니다는 [Azure Backup](backup-overview.md) Recovery Services 자격 증명 모음입니다. 종속성을 제거 자격 증명 모음을 삭제 하 고 강제로 자격 증명 모음을 삭제 하기 위한 지침을 포함 합니다.




## <a name="before-you-start"></a>시작하기 전에

시작 하기 전에 서버가 있는 Recovery Services 자격 증명 모음을 삭제할 수 없습니다는 이해, 등록 또는 백업 데이터를 보유 하는 중요 한 것입니다.


- 자격 증명 모음을 정상적으로 삭제 하려면에서 서버의 등록을 취소 하 고 자격 증명 모음 데이터를 제거 합니다.
- Recovery Services 자격 증명 모음에 있는 모든 데이터를 유지 하 고 자격 증명 모음을 삭제 하려면에 않으려면 강제로 자격 증명 모음을 삭제할 수 있습니다.
- 자격 증명 모음을 삭제하려고 해도 할 수 없는 경우 자격 증명 모음이 여전히 백업 데이터를 받도록 구성되어 있습니다.

자격 증명 모음을 삭제하는 방법을 알아보려면 [Azure Portal에서 자격 증명 모음 삭제](backup-azure-delete-vault.md#delete-a-vault-from-azure-portal) 섹션을 참조합니다. 경우 섹션인 [강제로 자격 증명 모음 삭제](backup-azure-delete-vault.md#delete-the-recovery-services-vault-by-force)합니다. 자격 증명 모음의 내용이 확실하지 않고 자격 증명 모음을 삭제할 수 있는지 확인해야 하는 경우 [자격 증명 모음 종속성 제거 및 자격 증명 모음 삭제](backup-azure-delete-vault.md#remove-vault-dependencies-and-delete-vault) 섹션을 참조합니다.

## <a name="delete-a-vault-from-the-azure-portal"></a>Azure portal에서 자격 증명 모음 삭제

1. 포털에서 Recovery Services 자격 증명 모음 목록을 엽니다.
2. 목록에서 삭제할 자격 증명 모음을 선택합니다. 자격 증명 모음 대시보드가 열립니다.

    ![대시보드를 열려면 자격 증명 모음 선택](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

1. 자격 증명 모음 대시보드에서 **삭제**합니다. 삭제할 것임을 확인 합니다.

    ![대시보드를 열려면 자격 증명 모음 선택](./media/backup-azure-delete-vault/click-delete-button-to-delete-vault.png)

2. 자격 증명 모음 종속성이 있으면 합니다 **삭제 오류 자격 증명 모음** 나타납니다. 

    ![자격 증명 모음 삭제 오류](./media/backup-azure-delete-vault/vault-delete-error.png)

    - 검토를 자격 증명 모음을 삭제 하기 전에 종속성을 제거 하려면 다음이 지침에 따라
    - [다음이 지침에 따라](#delete-the-recovery-services-vault-by-force) 강제로 자격 증명 모음을 삭제 하려면 PowerShell을 사용 하도록 합니다. 

## <a name="delete-the-recovery-services-vault-by-force"></a>Recovery Services 자격 증명 모음 강제 삭제

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

PowerShell을 사용하여 Recovery Services 자격 증명 모음을 강제로 삭제할 수 있습니다. 즉, 자격 증명 모음 및 연결 된 모든 백업 데이터를 영구적으로 삭제 됩니다. 

> [!Warning]
> Recovery Services 자격 증명 모음을 삭제 하려면 PowerShell을 사용 하는 경우 자격 증명 모음의 모든 백업 데이터를 영구적으로 삭제 되도록 확인 합니다.
>

Recovery Services 자격 증명 모음 삭제하려면

1. 사용 하 여 Azure 구독에 로그인 합니다 `Connect-AzAccount` 명령을 실행 하 고 수행는 화면의 지침.

   ```powershell
    Connect-AzAccount
   ```
2. 처음으로 Azure Backup을 사용 하 여, 구독에서 Azure Recovery Service 공급자를 등록 해야만 [레지스터 AzResourceProvider](/powershell/module/az.Resources/Register-azResourceProvider)합니다.

   ```powershell
    Register-AzResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
   ```

3. 관리자 권한으로 PowerShell 창을 엽니다.
4. `Set-ExecutionPolicy Unrestricted`를 사용하여 모든 제한을 제거합니다.
5. chocolately.org에서 Azure Resource Manager 클라이언트 패키지를 다운로드하려면 다음 명령을 실행합니다.

    `iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`

6. Azure Resource Manager API 클라이언트를 설치하려면 다음 명령을 사용합니다.

   `choco.exe install armclient`

7. Azure portal에서 삭제 하려는 자격 증명 모음에 대 한 구독 ID 및 리소스 그룹 이름을 수집 합니다.
8. PowerShell에서 사용자 구독 ID, 리소스 그룹 이름 및 자격 증명 모음 이름을 사용 하 여 다음 명령을 실행 합니다. 명령을 실행 하면 자격 증명 모음 및 모든 종속성을 삭제합니다.

   ```powershell
   ARMClient.exe delete /subscriptions/<subscriptionID>/resourceGroups/<resourcegroupname>/providers/Microsoft.RecoveryServices/vaults/<recovery services vault name>?api-version=2015-03-15
   ```
9. 자격 증명 모음의 비어 있지, "자격 증명 모음 수 없습니다.이 자격 증명이 모음 내에서 기존 리소스는 삭제 됨" 오류가 나타납니다. 자격 증명 모음 내에서 포함을 제거 하려면 다음을 수행 합니다.

   ```powershell
   ARMClient.exe delete /subscriptions/<subscriptionID>/resourceGroups/<resourcegroupname>/providers/Microsoft.RecoveryServices/vaults/<recovery services vault name>/registeredIdentities/<container name>?api-version=2016-06-01
   ```

10. Azure portal에서 구독에 로그인 하 고 데이터를 자격 증명 모음 삭제를 확인 합니다.


## <a name="remove-vault-dependencies-and-delete-vault"></a>자격 증명 모음 종속성 제거 및 자격 증명 모음 삭제

다음과 같이 자격 증명 모음 종속성을 수동으로 제거할 수 있습니다.

- 에 **Backup 항목** 메뉴, 제거 종속성:
    - Azure Storage(Azure 파일) 백업
    - Azure VM 백업의 SQL Server
    - Azure 가상 머신 백업
- 에 **Backup 인프라** 메뉴, 제거 종속성:
    - Microsoft Azure Backup Server (MABS) 백업
    - System Center DPM 백업

![대시보드를 열려면 자격 증명 모음 선택](./media/backup-azure-delete-vault/backup-items-backup-infrastructure.png)

### <a name="remove-backup-items"></a>백업 항목 제거

이 절차는 Azure files에서 백업 데이터를 제거 하는 방법을 보여 주는 예제를 제공 합니다.

1. 클릭 **Backup 항목** > **Azure Storage (Azure Files)**

    ![백업 유형 선택](./media/backup-azure-delete-vault/azure-storage-selected-list.png)

2. 각 Azure Files 항목을 제거 하 고 클릭 마우스 오른쪽 단추로 클릭 **백업 중지**합니다.

    ![백업 유형 선택](./media/backup-azure-delete-vault/stop-backup-item.png)


3. **Backup 중지** > **옵션을 선택**선택 **Backup 데이터 삭제**합니다.
4. 항목의 이름을 입력 하 고 클릭 **백업 중지**합니다. 
   - 이 항목을 삭제할 것인지 확인 합니다.
   - 합니다 **백업 중지** 확인 한 후 단추를 활성화 합니다.
   - 유지 하 고 데이터를 삭제 하지 마십시오 자격 증명 모음을 삭제할 수 없습니다.

     ![백업 데이터 삭제](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

5. 필요에 따라 데이터를 삭제 하는 이유는 이유를 제공 하 고 주석을 추가 합니다.
6. 삭제 작업이 완료 되었는지 확인 하려면 Azure 메시지 확인 ![백업 데이터 삭제](./media/backup-azure-delete-vault/messages.png).
7. 서비스 작업이 완료 되 면 메시지를 보냅니다: **백업 프로세스가 중지 되 고 백업 데이터가 삭제**합니다.
8. 목록에서 항목을 삭제한 후 **Backup 항목** 메뉴에서 **새로 고침**을 클릭하면 자격 증명 모음의 항목이 표시됩니다.

      ![백업 데이터 삭제](./media/backup-azure-delete-vault/empty-items-list.png)


### <a name="remove-backup-infrastructure-servers"></a>백업 인프라 서버 제거

1. 자격 증명 모음 대시보드 메뉴에서 클릭 **Backup 인프라**합니다.
2. 클릭 **Backup 관리 서버** 서버를 표시 합니다. 

    ![대시보드를 열려면 자격 증명 모음 선택](./media/backup-azure-delete-vault/delete-backup-management-servers.png)

2. 항목을 마우스 오른쪽 단추로 클릭 > **삭제**합니다.

    ![백업 유형 선택](./media/backup-azure-delete-vault/azure-storage-selected-list.png)

3. . **Backup 중지** > **옵션을 선택**선택 **Backup 데이터 삭제**합니다.
4. 항목의 이름을 입력 하 고 클릭 **백업 중지**합니다. 
   - 이 항목을 삭제할 것인지 확인 합니다.
   - 합니다 **백업 중지** 확인 한 후 단추를 활성화 합니다.
   - 유지 하 고 데이터를 삭제 하지 마십시오 자격 증명 모음을 삭제할 수 없습니다.

     ![백업 데이터 삭제](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

5. 필요에 따라 데이터를 삭제 하는 이유는 이유를 제공 하 고 주석을 추가 합니다.
6. 삭제 작업이 완료 되었는지 확인 하려면 Azure 메시지 확인 ![백업 데이터 삭제](./media/backup-azure-delete-vault/messages.png).
7. 서비스 작업이 완료 되 면 메시지를 보냅니다: **백업 프로세스가 중지 되 고 백업 데이터가 삭제**합니다.
8. 목록에서 항목을 삭제한 후 **Backup 항목** 메뉴에서 **새로 고침**을 클릭하면 자격 증명 모음의 항목이 표시됩니다.


### <a name="remove-azure-backup-agent-recovery-points"></a>Azure Backup 에이전트 복구 지점을 제거합니다

1. 자격 증명 모음 대시보드 메뉴에서 클릭 **Backup 인프라**합니다.
2. 클릭 **Backup 관리 서버** 인프라 서버를 표시 합니다.

    ![대시보드를 열려면 자격 증명 모음 선택](./media/backup-azure-delete-vault/identify-protected-servers.png)

3. **보호되는 서버** 목록에서 Azure Backup 에이전트를 클릭합니다.

    ![백업 유형 선택](./media/backup-azure-delete-vault/list-of-protected-server-types.png)

4. Azure Backup 에이전트를 사용 하 여 보호 된 서버의 목록에서 서버를 클릭 합니다.

    ![특정 보호된 서버 선택](./media/backup-azure-delete-vault/azure-backup-agent-protected-servers.png)

5. 선택한 서버 대시보드에서 **삭제**합니다.

    ![선택한 대시보드 삭제](./media/backup-azure-delete-vault/selected-protected-server-click-delete.png)

6. **삭제** 메뉴에서 항목의 이름을 입력하고 **삭제**를 클릭합니다.
   - 이 항목을 삭제할 것인지 확인 합니다.
   - 합니다 **백업 중지** 확인 한 후 단추를 활성화 합니다.
   - 유지 하 고 데이터를 삭제 하지 마십시오 자격 증명 모음을 삭제할 수 없습니다.

     ![백업 데이터 삭제](./media/backup-azure-delete-vault/delete-protected-server-dialog.png)

7. 필요에 따라 데이터를 삭제 하는 이유는 이유를 제공 하 고 주석을 추가 합니다.
8. 삭제 작업이 완료 되었는지 확인 하려면 Azure 메시지 확인 ![백업 데이터 삭제](./media/backup-azure-delete-vault/messages.png).
7. 서비스 작업이 완료 되 면 메시지를 보냅니다: **백업 프로세스가 중지 되 고 백업 데이터가 삭제**합니다.
8. 목록에서 항목을 삭제한 후 **Backup 항목** 메뉴에서 **새로 고침**을 클릭하면 자격 증명 모음의 항목이 표시됩니다.



### <a name="delete-the-vault-after-removing-dependencies"></a>종속성을 제거한 후 자격 증명 모음 삭제

1. 모든 종속성을 제거한 경우 스크롤하여 합니다 **Essentials** 자격 증명 모음 메뉴의 창.

    - 어떤 **Backup 항목**, **Backup 관리 서버** 또는 **복제된 항목**도 나열되지 않아야 합니다.
    - 자격 증명 모음에 항목이 아직 나타날를 제거 합니다.

2. 자격 증명 모음에 더 이상 항목이 없을 경우 자격 증명 모음 대시보드에서 **삭제**를 클릭합니다.

    ![백업 데이터 삭제](./media/backup-azure-delete-vault/vault-ready-to-delete.png)

1. 자격 증명 모음을 삭제할 것인지 확인하려면 **예**를 클릭합니다. 자격 증명 모음이 삭제되고 포털이 **새로 만들기** 서비스 메뉴로 돌아갑니다.

## <a name="what-if-i-stop-the-backup-process-but-retain-the-data"></a>백업 프로세스를 중지하지만 데이터가 남아 있는 경우?

백업 프로세스를 중지 해도 실수로 데이터를 유지 하는 경우에 이전 섹션에 설명 된 대로 백업 데이터를 삭제 해야 합니다.

## <a name="next-steps"></a>다음 단계

[에 대 한 자세한](backup-azure-recovery-services-vault-overview.md) Recovery Services 자격 증명 모음입니다.

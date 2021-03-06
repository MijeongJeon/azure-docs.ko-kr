---
title: PowerShell 예제 복원 백업 Azure SQL database | Microsoft Docs
description: 지역 중복 백업에서 Azure SQL 단일 데이터베이스를 복원하는 Azure PowerShell 예제 스크립트
services: sql-database
ms.service: sql-database
ms.subservice: backup-restore
ms.custom: ''
ms.devlang: PowerShell
ms.topic: sample
author: mashamsft
ms.author: mathoma
ms.reviewer: carlrab
manager: craigg
ms.date: 02/08/2019
ms.openlocfilehash: 730d944edfc16e9ef399333540b14fcfced4ce44
ms.sourcegitcommit: e69fc381852ce8615ee318b5f77ae7c6123a744c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "55996392"
---
# <a name="use-powershell-to-restore-an-azure-sql-single-database-from-backups"></a>PowerShell을 사용하여 백업에서 Azure SQL 단일 데이터베이스 복원

이 PowerShell 스크립트 예제는 지역 중복 백업에서 Azure SQL Database를 복원하고 삭제된 Azure SQL Database를 최신 백업으로 복원하며 Azure SQL Database를 특정 시점으로 복원합니다.  

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

PowerShell을 로컬로 설치하고 사용하도록 선택하는 경우 이 자습서에서는 Azure PowerShell 모듈 버전이 5.7.0 이상이어야 합니다. `Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다. 업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-az-ps)를 참조하세요. 또한 PowerShell을 로컬로 실행하는 경우 `Connect-AzureRmAccount`를 실행하여 Azure와 연결해야 합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a>배포 정리

스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. | [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | 단일 데이터베이스 또는 탄력적 풀을 호스트하는 SQL Database 서버를 만듭니다. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | SQL Database 서버의 데이터베이스를 단일 또는 풀링된 데이터베이스로 만듭니다. |
[Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | 단일 또는 풀링된 데이터베이스의 지역 중복 백업을 가져옵니다. |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | SQL 단일 또는 풀링된 데이터베이스를 복원합니다. |
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | Azure SQL 단일 또는 풀링된 데이터베이스를 제거합니다. |
| [Get AzureRmSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | 복원할 수 있는 삭제된 단일 또는 풀링된 데이터베이스를 가져옵니다. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.

추가 SQL Database PowerShell 스크립트 샘플은 [Azure SQL Database PowerShell 스크립트](../sql-database-powershell-samples.md)에 있습니다.

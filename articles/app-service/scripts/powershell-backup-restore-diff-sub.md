---
title: Azure PowerShell 스크립트 샘플 - 다른 구독의 앱 백업 복원 | Microsoft Docs
description: Azure PowerShell 스크립트 샘플 - 다른 구독에 있는 백업에서 웹앱 복원
services: app-service\web
documentationcenter: ''
author: msangapu
manager: jpconnoc
editor: ''
tags: azure-service-management
ms.assetid: a2a27d94-d378-4c17-a6a9-ae1e69dc4a72
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 11/21/2018
ms.author: msangapu
ms.custom: seodec18
ms.openlocfilehash: e8879b67b79523cc35fb28a707a6c77f3efb75c0
ms.sourcegitcommit: 7723b13601429fe8ce101395b7e47831043b970b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56584982"
---
# <a name="restore-a-web-app-from-a-backup-in-another-subscription-using-powershell"></a>PowerShell을 사용하여 다른 구독에 있는 백업에서 웹앱 복원

이 샘플 스크립트는 기존 웹앱에서 이전에 완료된 백업을 검색하고 다른 구독에 있는 웹앱으로 복원합니다. 

필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Connect-AzAccount`를 실행하여 Azure에 연결합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-restore-diff-sub/backup-restore-diff-sub.ps1?highlight=1-6 "Restore a web app from a backup in another subscription")]

## <a name="clean-up-deployment"></a>배포 정리 

더 이상 웹앱이 필요하지 않은 경우 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련 리소스를 제거할 수 있습니다.

```powershell
Remove-AzResourceGroup -Name $resourceGroupName -Force
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [Add-AzAccount](/powershell/module/az.accounts/connect-azaccount) | Azure Resource Manager cmdlet 요청에 사용할 인증된 계정을 추가합니다.  |
| [Get-AzWebAppBackupList](/powershell/module/az.websites/get-azwebappbackuplist) | 웹앱의 백업 목록을 가져옵니다. |
| [New-AzWebApp](/powershell/module/az.websites/new-azwebapp) | 웹앱 만들기 |
| [Restore-AzWebAppBackup](/powershell/module/az.websites/restore-azwebappbackup) | 이전에 완료된 백업에서 웹앱을 복원합니다. |

## <a name="next-steps"></a>다음 단계

Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.

Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../samples-powershell.md)에서 확인할 수 있습니다.

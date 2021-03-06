---
title: Azure CLI 스크립트 - Azure Database for MySQL 서버 복원
description: 이 샘플 Azure CLI 스크립트는 Azure Database for MySQL 서버 및 해당 데이터베이스를 이전 시점으로 복원하는 방법을 보여 줍니다.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.devlang: azurecli
ms.topic: sample
ms.custom: mvc
ms.date: 02/28/2018
ms.openlocfilehash: 7bc4b1533da272bed9b7b7b8a0abe9b509e02386
ms.sourcegitcommit: 71ee622bdba6e24db4d7ce92107b1ef1a4fa2600
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/17/2018
ms.locfileid: "53545113"
---
# <a name="restore-an-azure-database-for-mysql-server-using-azure-cli"></a>Azure CLI를 사용하여 Azure Database for MySQL 서버 복원
이 샘플 CLI 스크립트는 단일 Azure Database for MySQL 서버를 이전 시점으로 복원합니다.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

CLI를 로컬로 실행하도록 선택한 경우 이 문서에 Azure CLI 버전 2.0 이상이 필요합니다. `az --version`을 실행하여 버전을 확인합니다. Azure CLI 버전을 설치하거나 업그레이드하려면 [Azure CLI 설치]( /cli/azure/install-azure-cli)를 참조하세요. 

## <a name="sample-script"></a>샘플 스크립트
이 샘플 스크립트에서 강조 표시된 줄을 편집하여 관리자 사용자 이름 및 암호를 자신의 이름과 암호로 업데이트합니다. `az monitor` 명령에 사용된 구독 ID를 자신의 구독 ID로 바꿉니다.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/backup-restore.sh?highlight=15-16 "Restore Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a>배포 정리
스크립트가 실행 된 후 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거합니다. 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/backup-restore-pitr/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a>스크립트 설명
이 스크립트에는 다음 표에 설명된 명령이 사용됩니다.

| **명령** | **참고 사항** |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az mysql server create](/cli/azure/mysql/server#az-mysql-server-create) | 데이터베이스를 호스팅하는 MySQL 서버를 만듭니다. |
| [az mysql server restore](/cli/azure/mysql/server#az-mysql-server-restore) | 백업에서 서버를 복원합니다. |
| [az group delete](/cli/azure/group#az-group-delete) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계
- Azure CLI에 대한 자세한 내용: [Azure CLI 설명서](/cli/azure)
- 추가 스크립트 시도: [MySQL용 Azure Database에 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)

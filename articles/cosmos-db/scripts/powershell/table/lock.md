---
title: Azure Cosmos Table API 테이블에 대한 리소스 잠금을 만드는 PowerShell 스크립트
description: Azure Cosmos Table API 테이블에 대한 리소스 잠금 만들기
author: markjbrown
ms.author: mjbrown
ms.service: cosmos-db
ms.subservice: cosmosdb-table
ms.topic: sample
ms.date: 06/12/2020
ms.openlocfilehash: a35d2501eac631d34c7bf4d20ef775436a9d11c9
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99821567"
---
# <a name="create-a-resource-lock-for-azure-cosmos-table-api-table-using-azure-powershell"></a>Azure PowerShell을 사용하여 Azure Cosmos Table API 테이블에 대한 리소스 잠금 만들기
[!INCLUDE[appliesto-table-api](../../../includes/appliesto-table-api.md)]

[!INCLUDE [updated-for-az](../../../../../includes/updated-for-az.md)]

이 샘플에는 Azure PowerShell Az 5.4.0 이상이 필요합니다. `Get-Module -ListAvailable Az`를 실행하여 설치된 버전을 확인합니다.
설치해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-az-ps)를 참조하세요.

[Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount)를 실행하여 Azure에 로그인합니다.

> [!IMPORTANT]
> Cosmos DB SDK를 사용하여 연결하는 사용자가 만든 변경 내용, 계정 키를 통해 연결하는 모든 도구 또는 `disableKeyBasedMetadataWriteAccess` 속성을 사용하도록 설정하여 Cosmos DB 계정이 처음 잠겨 있지 않는 한 Azure Portal에서 리소스 잠금이 작동하지 않습니다. 이 속성을 사용하도록 설정하는 방법에 대한 자세한 내용은[Sdk변경 방지](../../../role-based-access-control.md#prevent-sdk-changes)를 참조하세요.

## <a name="sample-script"></a>샘플 스크립트

[!code-PowerShell[main](../../../../../PowerShell_scripts/cosmosdb/table/ps-table-lock.ps1 "Create, list, and remove resource locks")]

## <a name="clean-up-deployment"></a>배포 정리

스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.

```PowerShell
Remove-AzResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
|**Azure 리소스**| |
| [New-AzResourceLock](/PowerShell/module/az.resources/new-azresourcelock) | 리소스 잠금을 만듭니다. |
| [Get-AzResourceLock](/PowerShell/module/az.resources/get-azresourcelock) | 리소스 잠금을 가져오거나 리소스 잠금을 나열합니다. |
| [Remove-AzResourceLock](/PowerShell/module/az.resources/remove-azresourcelock) | 리소스 잠금을 제거합니다. |
|||

## <a name="next-steps"></a>다음 단계

Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/PowerShell/)를 참조하세요.
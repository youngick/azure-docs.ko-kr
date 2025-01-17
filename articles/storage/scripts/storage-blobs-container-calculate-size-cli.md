---
title: Azure CLI 스크립트 샘플 - Blob 컨테이너 크기 계산 | Microsoft Docs
description: 컨테이너에 있는 Blob의 크기를 합계해서 Azure Blob Storage의 컨테이너 크기를 계산합니다.
services: storage
author: tamram
ms.service: storage
ms.subservice: blobs
ms.devlang: cli
ms.topic: sample
ms.date: 06/28/2017
ms.author: tamram
ms.custom: devx-track-azurecli
ms.openlocfilehash: 45712632ebfb2da4b713038503965ce908c1dfc6
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87498891"
---
# <a name="calculate-the-size-of-a-blob-storage-container"></a>Blob Storage 컨테이너 크기 계산

이 스크립트는 컨테이너에 있는 Blob의 크기를 합계해서 Azure Blob Storage의 컨테이너 크기를 계산합니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

> [!IMPORTANT]
> 이 CLI 스크립트는 컨테이너의 예상 크기를 제공하므로 청구 요금 계산에 사용하면 안 됩니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli[main](../../../cli_scripts/storage/calculate-container-size/calculate-container-size.sh?highlight=2-3 "Calculate container size")]

## <a name="clean-up-deployment"></a>배포 정리

다음 명령을 실행하여 리소스 그룹, 컨테이너 및 모든 관련된 리소스를 제거합니다.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용하여 Blob Storage 컨테이너의 크기를 계산합니다. 표에 있는 각 항목은 명령 관련 설명서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [az group create](/cli/azure/group) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az storage blob upload](/cli/azure/storage/account) | Azure Blob Storage 컨테이너에 로컬 파일을 업로드합니다. |
| [az storage blob list](/cli/azure/storage/account/keys) | Azure Blob Storage 컨테이너의 Blob을 나열합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure)를 참조하세요.

추가 스토리지 CLI 스크립트 샘플은 [Azure Blob Storage에 대한 Azure CLI 샘플](../blobs/storage-samples-blobs-cli.md)에서 찾을 수 있습니다.

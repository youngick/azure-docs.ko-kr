---
title: Azure CLI - 랩에서 가상 머신 만들기 및 확인
description: 이 Azure CLI 스크립트는 랩에서 가상 머신을 만들고 사용 가능한지 확인합니다.
ms.devlang: azurecli
ms.topic: sample
ms.date: 08/11/2020
ms.openlocfilehash: c7625f62d7897d61903f864b216ccf9aa13648ea
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102198424"
---
# <a name="use-azure-cli-to-create-and-verify-availability-of-a-virtual-machine-in-a-lab-in-azure-devtest-labs"></a>Azure CLI를 사용하여 Azure DevTest Labs의 랩에서 가상 머신을 만들고 사용 가능성 확인

이 Azure CLI 스크립트는 랩에서 VM(가상 머신)을 만듭니다. ssh 인증을 사용하여 Marketplace 이미지를 기반으로 만들어진 VM. 그런 다음 스크립트는 VM이 사용 가능한지 확인합니다. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/devtest-lab/create-verify-virtual-machine-in-lab/create-verify-virtual-machine-in-lab.sh "Create and verify availability of a VM")]

## <a name="clean-up-deployment"></a>배포 정리 

다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다.

| 명령 | 메모 |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az lab vm create](/cli/azure/lab/vm#az-lab-vm-create) | 랩에서 VM(가상 머신)을 만듭니다. |
| [az lab vm show](/cli/azure/lab/vm#az-lab-vm-show) | 랩에서 VM의 상태를 표시합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure)를 참조하세요.

추가 Azure Lab Services CLI 스크립트 샘플은 [Azure Lab Services CLI 샘플](../samples-cli.md)에서 확인할 수 있습니다.

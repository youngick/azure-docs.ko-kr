---
title: Azure CLI 샘플 - 호스트 기반 자동 크기 조정 사용
description: 이 스크립트는 Ubuntu를 실행하는 가상 머신 확장 집합을 만들고, CPU 로드 변경에 따라 호스트 기반 메트릭을 사용하여 자동으로 크기 조정합니다.
author: ju-shim
tags: azure-resource-manager
ms.service: virtual-machine-scale-sets
ms.subservice: autoscale
ms.devlang: azurecli
ms.topic: sample
ms.date: 03/27/2018
ms.author: jushiman
ms.custom: mvc, devx-track-azurecli
ms.openlocfilehash: 8e8118a32da296d090ba22122b5188f941419e94
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87502140"
---
# <a name="automatically-scale-a-virtual-machine-scale-set-with-the-azure-cli"></a>Azure CLI를 사용하여 가상 머신 확장 집합의 크기 자동 조정
이 스크립트는 Ubuntu를 실행하는 가상 머신 확장 집합을 만들고, CPU 로드 변경에 따라 호스트 기반 메트릭을 사용하여 자동으로 크기 조정합니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트
[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine-scale-sets/auto-scale-host-metrics/auto-scale-host-metrics.sh "Automatically scale a virtual machine scale set")]

## <a name="clean-up-deployment"></a>배포 정리
다음 명령을 실행하여 리소스 그룹, 확장 집합 및 모든 관련된 리소스를 제거할 수 있습니다.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명
이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 머신 확장 집합 및 관련된 모든 리소스를 만듭니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [az group create](/cli/azure/ad/group) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az vmss create](/cli/azure/vmss) | 가상 머신 확장 집합을 만들고 가상 네트워크, 서브넷 및 네트워크 보안 그룹에 연결합니다. 부하 분산 장치도 여러 VM 인스턴스에 트래픽을 분산하기 위해 만듭니다. 또한 이 명령은 사용할 VM 이미지와 관리 자격 증명도 지정합니다.  |
| [az monitor autoscale-settings create](/cli/azure/monitor/autoscale-settings) | 자동 크기 조정 규칙을 만들고 가상 머신 확장 집합에 적용합니다. |
| [az group delete](/cli/azure/ad/group) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계
Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.

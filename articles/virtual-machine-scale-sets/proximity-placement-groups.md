---
title: 가상 머신 확장 집합에 대한 근접 배치 그룹 미리 보기
description: Azure에서 Windows 가상 머신 확장 집합에 대한 근접 배치 그룹을 만들고 사용하는 방법을 알아봅니다.
author: cynthn
ms.author: cynthn
ms.topic: how-to
ms.service: virtual-machine-scale-sets
ms.subservice: availability
ms.date: 07/01/2019
ms.reviewer: zivr
ms.custom: mimckitt
ms.openlocfilehash: a3a7b50c82b3deffa7526bfcfe799972c3b02762
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98877869"
---
# <a name="preview-creating-and-using-proximity-placement-groups-using-powershell"></a>미리 보기: PowerShell을 사용하여 근접 배치 그룹 만들기 및 사용

VM을 가능한 가깝게 유지하여 가장 낮은 대기 시간을 달성하려면 [근접 배치 그룹](../virtual-machines/co-location.md#proximity-placement-groups) 내에 확장 집합을 배포해야 합니다.

근접 배치 그룹은 Azure 컴퓨팅 리소스가 물리적으로 서로 가까운 위치에 있도록 하는 데 사용되는 논리적 그룹화입니다. 근접 배치 그룹은 낮은 대기 시간을 요구하는 작업에 유용합니다.

> [!IMPORTANT]
> 근접 배치 그룹은 현재 퍼블릭 미리 보기 상태입니다.
> 이 미리 보기 버전은 서비스 수준 계약 없이 제공되며 프로덕션 워크로드에는 사용하지 않는 것이 좋습니다. 특정 기능이 지원되지 않거나 기능이 제한될 수 있습니다. 자세한 내용은 [Microsoft Azure Preview에 대한 추가 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.
>
> 미리 보기 중에 근접 배치 그룹을 사용할 수 없는 지역은 **일본 동부**, **오스트레일리아 동부** 및 **인도 중부** 입니다.


## <a name="create-a-proximity-placement-group"></a>근접 배치 그룹 만들기
[New-AzProximityPlacementGroup](/powershell/module/az.compute/new-azproximityplacementgroup) cmdlet을 사용하여 근접 배치 그룹을 만듭니다. 

```azurepowershell-interactive
$resourceGroup = "myPPGResourceGroup"
$location = "East US"
$ppgName = "myPPG"
New-AzResourceGroup -Name $resourceGroup -Location $location
$ppg = New-AzProximityPlacementGroup `
   -Location $location `
   -Name $ppgName `
   -ResourceGroupName $resourceGroup `
   -ProximityPlacementGroupType Standard
```

## <a name="list-proximity-placement-groups"></a>근접 배치 그룹 나열

[Get-AzProximityPlacementGroup](/powershell/module/az.compute/get-azproximityplacementgroup) cmdlet을 사용하여 모든 근접 배치 그룹을 나열할 수 있습니다.

```azurepowershell-interactive
Get-AzProximityPlacementGroup
```


## <a name="create-a-scale-set"></a>확장 집합 만들기

[New-AzVMSS](/powershell/module/az.compute/new-azvmss)를 사용하여 확장 집합을 만들 경우 `-ProximityPlacementGroup $ppg.Id`로 근접 배치 그룹 ID를 참조하여 근접 배치 그룹에 확장 집합을 만듭니다.

```azurepowershell-interactive
$scalesetName = "myVM"

New-AzVmss `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -VMScaleSetName $scalesetName `
  -VirtualNetworkName "myVnet" `
  -SubnetName "mySubnet" `
  -PublicIpAddressName "myPublicIPAddress" `
  -LoadBalancerName "myLoadBalancer" `
  -UpgradePolicyMode "Automatic" `
  -ProximityPlacementGroup $ppg.Id
```

[Get-AzProximityPlacementGroup](/powershell/module/az.compute/get-azproximityplacementgroup)을 사용하여 배치 그룹에서 인스턴스를 볼 수 있습니다.

```azurepowershell-interactive
  Get-AzProximityPlacementGroup `
   -ResourceId $ppg.Id | Format-Table `
   -Wrap `
   -Property VirtualMachineScaleSets
```

## <a name="next-steps"></a>다음 단계

또한 [Azure CLI](../virtual-machines/linux/proximity-placement-groups.md)를 사용하여 근접 배치 그룹을 만들 수도 있습니다.

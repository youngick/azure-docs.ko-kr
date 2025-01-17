---
title: Azure PowerShell을 사용하여 가용성 집합에 VM 배포
description: Azure PowerShell을 사용하여 가용성 집합에서 고가용성 가상 머신을 배포하는 방법 알아보기
services: virtual-machines
author: mimckitt
ms.service: virtual-machines
ms.topic: how-to
ms.date: 3/8/2021
ms.author: mimckitt
ms.reviewer: cynthn
ms.custom: mvc
ms.openlocfilehash: 178a29ea37195ddd2013ca5220663a75132beb24
ms.sourcegitcommit: e6de1702d3958a3bea275645eb46e4f2e0f011af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102555910"
---
# <a name="create-and-deploy-virtual-machines-in-an-availability-set-using-azure-powershell"></a>Azure PowerShell을 사용하여 가용성 집합에서 가상 머신 만들기 및 배포

이 자습서에서는 가용성 집합을 사용하여 VM(Virtual Machine)의 가용성과 안정성을 향상시키는 방법에 대해 알아봅니다. 가용성 집합은 Azure에 배포한 VM이 클러스터의 격리된 여러 하드웨어 노드에 분산되어 있는지 확인합니다. 

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
> * 가용성 집합 만들기
> * 가용성 집합에서 VM 만들기
> * 사용 가능한 VM 크기 확인
> * Azure Advisor 확인


## <a name="launch-azure-cloud-shell"></a>Azure Cloud Shell 시작

Azure Cloud Shell은 이 항목의 단계를 실행하는 데 무료로 사용할 수 있는 대화형 셸입니다. 공용 Azure 도구가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다. 

Cloud Shell을 열려면 코드 블록의 오른쪽 위 모서리에 있는 **사용해 보세요** 를 선택하기만 하면 됩니다. 또한 [https://shell.azure.com/powershell](https://shell.azure.com/powershell)로 이동하여 별도의 브라우저 탭에서 Cloud Shell을 시작할 수도 있습니다. **복사** 를 선택하여 코드 블록을 복사하여 Cloud Shell에 붙여넣고, Enter 키를 눌러 실행합니다.

## <a name="create-an-availability-set"></a>가용성 집합 만들기

한 위치의 하드웨어는 여러 개의 업데이트 도메인 및 장애 도메인으로 구분됩니다. **업데이트 도메인** 은 동시에 다시 부팅할 수 있는 VM 그룹과 기본 물리적 하드웨어입니다. 동일한 **장애 도메인** 의 VM은 공통의 스토리지뿐만 아니라 공통의 전원 및 네트워크 스위치를 공유합니다.  

[New-AzAvailabilitySet](/powershell/module/az.compute/new-azavailabilityset)을 사용하여 가용성 집합을 만들 수 있습니다. 이 예제에서 업데이트 및 장애 도메인의 수는 모두 *2* 이며 가용성 집합의 이름은 *myAvailabilitySet* 입니다.

리소스 그룹을 만듭니다.

```azurepowershell-interactive
New-AzResourceGroup `
   -Name myResourceGroupAvailability `
   -Location EastUS
```

`-sku aligned` 매개 변수가 있는 [New-AzAvailabilitySet](/powershell/module/az.compute/new-azavailabilityset)을 사용하여 관리형 가용성 집합을 만듭니다.

```azurepowershell-interactive
New-AzAvailabilitySet `
   -Location "EastUS" `
   -Name "myAvailabilitySet" `
   -ResourceGroupName "myResourceGroupAvailability" `
   -Sku aligned `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>가용성 집합에 포함된 VM 만들기
VM이 하드웨어 전체에 올바르게 배포되도록 하려면 VM을 가용성 집합 내에 만들어야 합니다. VM을 만든 후에는 가용성 집합에 기존 VM을 추가할 수 없습니다. 


[New-AzVM](/powershell/module/az.compute/new-azvm)을 사용하여 VM을 만들 때 `-AvailabilitySetName` 매개 변수를 사용하여 가용성 집합의 이름을 지정합니다.

먼저 [Get-Credential](/powershell/module/microsoft.powershell.security/get-credential)을 사용하여 VM에 대한 관리자 사용자 이름과 암호를 설정합니다.

```azurepowershell-interactive
$cred = Get-Credential
```

이제 [New-AzVM](/powershell/module/az.compute/new-azvm)을 사용하여 가용성 집합에 2개의 VM을 만듭니다.

```azurepowershell-interactive
for ($i=1; $i -le 2; $i++)
{
    New-AzVm `
        -ResourceGroupName "myResourceGroupAvailability" `
        -Name "myVM$i" `
        -Location "East US" `
        -VirtualNetworkName "myVnet" `
        -SubnetName "mySubnet" `
        -SecurityGroupName "myNetworkSecurityGroup" `
        -PublicIpAddressName "myPublicIpAddress$i" `
        -AvailabilitySetName "myAvailabilitySet" `
        -Credential $cred
}
```

두 VM을 만들고 구성하는 데 몇 분 정도 소요됩니다. 완료되면 기본 하드웨어에 2개의 가상 머신이 배포되어 있습니다. 

**리소스 그룹** > **myResourceGroupAvailability** > **myAvailabilitySet** 으로 차례로 이동하여 포털에서 가용성 집합을 살펴보면 VM이 2개의 장애 및 업데이트 도메인에 배포되는 방식을 확인할 수 있습니다.

![포털의 가용성 집합](./media/tutorial-availability-sets/fd-ud.png)

## <a name="check-for-available-vm-sizes"></a>사용 가능한 VM 크기 확인 

가용성 집합 내에서 VM을 만들 때는 하드웨어에서 사용할 수 있는 VM 크기를 알아야 합니다. [Get-AzVMSize](/powershell/module/az.compute/get-azvmsize) 명령을 사용하여 가용성 집합에 배포할 수 있는 가상 머신에 사용할 수 있는 모든 크기를 가져옵니다.

```azurepowershell-interactive
Get-AzVMSize `
   -ResourceGroupName "myResourceGroupAvailability" `
   -AvailabilitySetName "myAvailabilitySet"
```

## <a name="check-azure-advisor"></a>Azure Advisor 확인 

또한 Azure Advisor를 사용하여 VM의 가용성을 개선하는 방법에 대한 자세한 정보를 볼 수 있습니다. Azure Advisor는 구성 및 사용량 원격 분석을 수행한 다음, Azure 리소스의 비용 효율성, 성능, 가용성 및 보안을 향상시키는 데 도움이 되는 해결 방법을 권장합니다.

[Azure Portal](https://portal.azure.com)에 로그인하고, **모든 서비스** 를 선택하고, **Advisor** 를 입력합니다. Advisor 대시보드에 선택한 구독에 대해 맞춤형 추천이 표시됩니다. 자세한 내용은 [Azure Advisor 시작](../../advisor/advisor-get-started.md)을 참조하세요.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.

> [!div class="checklist"]
> * 가용성 집합 만들기
> * 가용성 집합에서 VM 만들기
> * 사용 가능한 VM 크기 확인
> * Azure Advisor 확인

가상 머신 확장 집합에 대해 알아보려면 다음 자습서로 이동합니다.

> [!div class="nextstepaction"]
> [VM 확장 집합 만들기](tutorial-create-vmss.md)

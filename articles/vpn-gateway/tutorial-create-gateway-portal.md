---
title: '자습서 - VPN Gateway 만들기 및 관리: Azure portal'
description: 이 자습서에 따라 포털을 사용하여 Azure VPN Gateway를 만들고, 배포하고, 관리하는 방법을 알아봅니다.
author: cherylmc
ms.author: cherylmc
ms.service: vpn-gateway
ms.topic: tutorial
ms.date: 12/01/2020
ms.openlocfilehash: 820482a268af038737557c517ccda086cd65d943
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99822257"
---
# <a name="tutorial-create-and-manage-a-vpn-gateway-using-azure-portal"></a>자습서: Azure Portal을 사용하여 VPN 게이트웨이 만들기 및 관리

Azure VPN 게이트웨이는 고객 프레미스와 Azure 사이에 프레미스 간 연결을 제공합니다. 이 자습서에서는 VPN 게이트웨이 만들기 및 관리 같은 기본적인 Azure VPN 게이트웨이 배포 항목을 다룹니다. [Azure CLI](create-routebased-vpn-gateway-cli.md) 또는 [Azure PowerShell](create-routebased-vpn-gateway-powershell.md)을 사용하여 게이트웨이를 만들 수도 있습니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
> * 가상 네트워크 만들기
> * VPN 게이트웨이 만들기
> * 게이트웨이 공용 IP 주소 보기
> * VPN 게이트웨이 크기 조정(SKU 크기 조정)
> * VPN Gateway 다시 설정

다음 다이어그램은 이 자습서에서 만든 가상 네트워크 및 VPN 게이트웨이를 보여줍니다.

:::image type="content" source="./media/tutorial-create-gateway-portal/gateway-diagram.png" alt-text="VNet 및 VPN 게이트웨이 다이어그램":::

## <a name="prerequisites"></a>필수 구성 요소

활성 구독이 있는 Azure 계정. 계정이 없는 경우 [체험 계정을 만듭니다](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).

## <a name="create-a-virtual-network"></a><a name="CreatVNet"></a>가상 네트워크 만들기

다음 값을 사용하여 VNet을 만듭니다.

* **리소스 그룹:** TestRG1
* **이름:** VNet1
* **지역:** (미국) 미국 동부
* **IPv4 주소 공간:** 10.1.0.0/16
* **서브넷 이름:** FrontEnd
* **서브넷 주소 공간:** 10.1.0.0/24

[!INCLUDE [Create a virtual network](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="create-a-vpn-gateway"></a><a name="VNetGateway"></a>VPN 게이트웨이 만들기

이 단계에서는 VNet용 가상 네트워크 게이트웨이를 만듭니다. 종종 선택한 게이트웨이 SKU에 따라 게이트웨이를 만드는 데 45분 이상 걸릴 수 있습니다.

다음 값을 사용하여 가상 네트워크 게이트웨이를 만듭니다.

* **이름:** VNet1GW
* **지역:** 미국 동부
* **게이트웨이 유형:** VPN
* **VPN 유형:** 경로 기반
* **SKU:** VpnGw1
* **생성:** Generation1
* **가상 네트워크:** VNet1
* **게이트웨이 서브넷 주소 범위:** 10.1.255.0/27
* **공용 IP 주소:** 새로 만들기
* **공용 IP 주소 이름:** VNet1GWpip
* **active-active 모드를 사용하도록 설정:** 사용 안 함
* **BGP 구성:** 사용 안 함

[!INCLUDE [Create a vpn gateway](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

[!INCLUDE [NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="view-the-public-ip-address"></a><a name="view"></a>공용 IP 주소 보기

게이트웨이의 **개요** 페이지에서 게이트웨이 공용 IP 주소를 볼 수 있습니다.

:::image type="content" source="./media/tutorial-create-gateway-portal/address.png" alt-text="개요 페이지":::

공용 IP 주소 개체에 대한 추가 정보를 보려면 **공용 IP 주소** 옆에 있는 이름/IP 주소 링크를 클릭합니다.

## <a name="resize-a-gateway-sku"></a><a name="resize"></a>게이트웨이 SKU 크기 조정

크기 조정 및 게이트웨이 SKU 변경과 관련된 특정 규칙이 있습니다. 이 섹션에서는 SKU의 크기를 조정합니다. 자세한 내용은 [게이트웨이 설정 - SKU 크기 조정 및 변경](vpn-gateway-about-vpn-gateway-settings.md#resizechange)을 참조하세요.

[!INCLUDE [resize a gateway](../../includes/vpn-gateway-resize-gw-portal-include.md)]

## <a name="reset-a-gateway"></a><a name="reset"></a>게이트웨이 다시 설정

[!INCLUDE [reset a gateway](../../includes/vpn-gateway-reset-gw-portal-include.md)]

## <a name="clean-up-resources"></a>리소스 정리

이 애플리케이션을 계속 사용하지 않거나 다음 자습서로 이동하지 않으려면 다음 단계에 따라 해당 리소스를 삭제합니다.

1. 포털 위쪽의 **검색** 상자에서 리소스 그룹 이름을 입력하고, 검색 결과에서 이를 선택합니다.

1. **리소스 그룹 삭제** 를 선택합니다.

1. **리소스 그룹 이름 입력** 에 대해 리소스 그룹을 입력하고, **삭제** 를 선택합니다.

## <a name="next-steps"></a>다음 단계

VPN 게이트웨이가 있으면 연결을 구성할 수 있습니다. 다음 문서는 가장 일반적인 구성 몇 가지를 만드는 데 도움이 됩니다.

> [!div class="nextstepaction"]
> [사이트 간 VPN 연결](./tutorial-site-to-site-portal.md)

> [!div class="nextstepaction"]
> [지점 및 사이트 간 VPN 연결](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
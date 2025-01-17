---
title: 포함 파일
description: 포함 파일
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 12/06/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 4732abacc80a24d268f0e5cb7d100079e5a8d90b
ms.sourcegitcommit: ed7376d919a66edcba3566efdee4bc3351c57eda
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105104141"
---
원격 데스크톱 연결을 만들어 VNet에 배포된 VM에 연결합니다. VM에 연결할 수 있는지 확인하는 가장 좋은 방법은 컴퓨터 이름이 아닌 개인 IP 주소를 사용하여 연결하는 것입니다. 이렇게 하면 연결할 수 있는지, 아니면 이름 확인이 제대로 구성되었는지를 테스트할 수 있습니다. 

1. VM의 개인 IP 주소를 찾습니다. VM의 개인 IP 주소를 찾으려면 Azure Portal에서 VM의 속성을 보거나 PowerShell을 사용합니다.
2. 지점 및 사이트 간 VPN 연결을 사용하여 VNet에 연결되어 있는지 확인합니다. 
3. 원격 데스크톱 연결을 열려면 작업 표시줄의 검색 상자에서 *RDP* 또는 *원격 데스크톱 연결* 을 입력한 다음, **원격 데스크톱 연결** 을 선택합니다. 또한 PowerShell에서 **mstsc** 명령을 사용하여 원격 데스크톱 연결을 열 수도 있습니다. 
3. **원격 데스크톱 연결** 에서 VM의 개인 IP 주소를 입력 합니다. 필요한 경우 **옵션 표시** 를 선택하여 추가 설정을 조정한 다음, 연결합니다.

### <a name="to-troubleshoot-an-rdp-connection-to-a-vm"></a>VM에 대한 RDP 연결 문제를 해결하려면

VPN 연결을 통해 가상 머신에 연결하는 데 문제가 있는 경우 이를 확인할 수 있는 몇 가지 방법이 있습니다. 

- VPN 연결이 성공했는지 확인합니다.
- VM의 개인 IP 주소에 연결하고 있는지 확인합니다.
- **ipconfig** 를 입력하여 연결하는 컴퓨터의 이더넷 어댑터에 할당된 IPv4 주소를 확인합니다. IP 주소가 연결하는 VNet의 주소 범위 또는 VPNClientAddressPool의 주소 범위 내에 있으면 겹치는 주소 공간이 발생합니다. 주소 공간이 이러한 방식으로 겹치면 네트워크 트래픽이 Azure에 도달하지 않고 로컬 네트워크에 남아 있습니다.
- 컴퓨터 이름이 아닌 개인 IP 주소를 사용하여 VM에 연결할 수 있으면 DNS를 올바르게 구성했는지 확인합니다. 이름 확인이 VM에서 작동하는 방법에 대한 자세한 내용은 [VM에서 이름 확인](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.
- VNet에 대한 DNS 서버 IP 주소가 지정되면 VPN 클라이언트 구성 패키지가 생성되는지 확인합니다. DNS 서버 IP 주소를 업데이트하는 경우 새 VPN 클라이언트 구성 패키지를 생성하고 설치합니다.

자세한 문제 해결 정보는 [VM에 대한 원격 데스크톱 연결 문제 해결](/troubleshoot/azure/virtual-machines/troubleshoot-rdp-connection)을 참조하세요.
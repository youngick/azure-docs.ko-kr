---
title: Azure Virtual Network NAT에 대 한 메트릭 및 경고
titleSuffix: Azure Virtual Network
description: Virtual Network NAT에 사용할 수 있는 Azure Monitor 메트릭 및 경고를 이해 합니다.
services: virtual-network
documentationcenter: na
author: asudbring
manager: KumudD
ms.service: virtual-network
ms.subservice: nat
Customer intent: As an IT administrator, I want to understand available Azure Monitor metrics and alerts for Virtual Network NAT.
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/04/2020
ms.author: allensu
ms.openlocfilehash: e3c47a60a6cda074eba7b5c3292577c29f50c2ab
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87424054"
---
# <a name="azure-virtual-network-nat-metrics"></a>Azure Virtual Network NAT 메트릭

Azure Virtual Network NAT 게이트웨이 리소스는 다차원 메트릭을 제공 합니다. 이러한 메트릭을 사용 하 여 작업을 관찰 하 고 [문제를 해결할](troubleshoot-nat.md)수 있습니다.  SNAT 고갈와 같은 중요 한 문제에 대해 경고를 구성할 수 있습니다.

<p align="center">
  <img src="media/nat-overview/flow-direction1.svg" alt="Figure depicts a NAT gateway resource that consumes all IP addresses for a public IP prefix and directs that traffic to and from two subnets of virtual machines and a virtual machine scale set." width="256" title="인터넷으로의 아웃바운드를 위한 Virtual Network NAT">
</p>

*그림: 인터넷으로의 아웃바운드를 위한 Virtual Network NAT*

## <a name="metrics"></a>메트릭

NAT 게이트웨이 리소스는 Azure Monitor에서 다음과 같은 다차원 메트릭을 제공 합니다.

| 메트릭 | 설명 | 권장 집계 | 차원 |
|---|---|---|---|
| 바이트 | 인바운드 및 아웃 바운드 처리 된 바이트 | 합계 | 방향 ( Out), 프로토콜 (6 TCP, 17 UDP) |
| 패킷 수 | 인바운드 및 아웃 바운드 처리 된 패킷 | 합계 | 방향 ( Out), 프로토콜 (6 TCP, 17 UDP) |
| 삭제 된 패킷 | NAT 게이트웨이에서 삭제 된 패킷 | 합계 | / |
| SNAT 연결 수 | 간격 당 상태 전환 | 합계 | 연결 상태, 프로토콜 (6 TCP, 17 UDP) |
| 총 SNAT 연결 수 | 현재 활성 SNAT 연결 (~ SNAT 포트 사용) | 합계 | 프로토콜 (6 TCP, 17 UDP) |


## <a name="alerts"></a>경고

메트릭에 대 한 경고는 위의 각 [메트릭에](#metrics)대 한 Azure Monitor에서 구성할 수 있습니다.

## <a name="limitations"></a>제한 사항

Resource Health 지원 되지 않습니다.

## <a name="next-steps"></a>다음 단계

* [Virtual Network NAT](nat-overview.md)에 대한 자세한 정보
* [NAT 게이트웨이 리소스](nat-gateway-resource.md)에 대한 자세한 정보
* [Azure Monitor](../azure-monitor/overview.md) 에 대해 알아보기
* [NAT 게이트웨이 리소스 문제 해결](troubleshoot-nat.md)에 대해 알아봅니다.
* [UserVoice에서 Virtual Network NAT에 대해 다음에 빌드할 항목을 알려줍니다](https://aka.ms/natuservoice).



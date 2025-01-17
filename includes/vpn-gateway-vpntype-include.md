---
title: 파일 포함
description: 파일 포함
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: b3907882df09bfae1d6453fbffbd3e7562554f7c
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96010884"
---
* **정책 기반** : 정책 기반 VPN은 이전에 호출된 클래식 배포 모델에서 고정 라우팅 게이트웨이였습니다. 정책 기반 VPN은 온-프레미스 네트워크와 Azure VNet 간의 주소 접두사의 조합으로 구성된 IPsec 정책에 따라 IPsec 터널을 통해 패킷을 암호화하고 전달합니다. 정책(또는 트래픽 선택기)는 일반적으로 VPN 디바이스 구성에서 액세스 목록으로 정의됩니다. 정책 기반 VPN 유형에 대한 값은 *PolicyBased* 입니다. PolicyBased VPN을 사용할 때는 다음과 같은 제한에 유의하세요.
  
  * PolicyBased VPN은 기본 게이트웨이 SKU에서 **만** 사용할 수 있습니다. 이 VPN 유형은 다른 게이트웨이 SKU와 호환되지 않습니다.
  * PolicyBased VPN을 사용하는 경우 터널 1개만 허용됩니다.
  * S2S 연결 및 특정 구성에 대해서만 PolicyBased VPN을 사용할 수 있습니다. 대부분의 VPN Gateway 구성에는 RouteBased VPN이 필요합니다.
* **경로 기반**: 경로 기반 VPN은 이전에 호출된 클래식 배포 모델에서 동적 라우팅 게이트웨이였습니다. 경로 기반 VPN은 IP 전달 또는 라우팅 테이블에서 “경로"를 사용하여 패킷을 해당 터널 인터페이스에 전달합니다. 그런 다음 터널 인터페이스는 터널로 들어오는 터널에서 나가는 패킷을 암호화하거나 암호 해독합니다. 경로 기반 VPN에 대한 정책(또는 트래픽 선택기)은 임의 또는 와일드카드로 구성됩니다. 경로 기반 VPN 유형에 대한 값은 *RouteBased* 입니다.

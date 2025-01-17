---
title: 파일 포함
description: 포함 파일
services: virtual-machines-windows
author: cynthn
ms.service: virtual-machines-windows
ms.topic: include
ms.date: 09/12/2018
ms.author: cynthn
ms.custom: include file
ms.openlocfilehash: ec6cbcbc93fe87634c87caeb0041b75ec916a22f
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "67182173"
---
서브넷 또는 VM 네트워크 인터페이스에서 네트워크 필터를 만들어, Azure에서 VM(가상 머신)에 대한 포트를 열거나 엔드포인트를 만듭니다. 인바운드 및 아웃바운드 트래픽을 모두 제어하는 이러한 필터를 트래픽을 수신하는 리소스에 연결된 네트워크 보안 그룹에 배치합니다.

이 문서에 있는 예제에서 표준 TCP 포트 80(해당 서비스를 이미 시작했으며 VM에서 OS 방화벽 규칙을 열었다고 가정함)을 사용하는 네트워크 필터를 작성하는 방법을 보여 줍니다.

표준 TCP 포트 80에서 웹 요청을 제공하도록 구성된 VM을 만든 후 다음을 수행할 수 있습니다.

1. 네트워크 보안 그룹을 만듭니다.

2. 트래픽을 허용하는 인바운드 보안 규칙을 작성하고 다음 설정에 값을 지정하세요.

   - **대상 포트 범위**: 80

   - **소스 포트 범위**: *(모든 소스 포트 허용)

   - **우선 순위 값**: 65,500 미만이고 기본 catch-all 거부 인바운드 규칙보다 우선 순위에서 상위에 있는 값을 입력하세요.

3. 네트워크 보안 그룹을 VM 네트워크 인터페이스 또는 서브넷에 연결합니다.

이 예제에서는 HTTP 트래픽을 허용하는 단순 규칙을 사용하지만 네트워크 보안 그룹 및 규칙을 사용하여 더 복잡한 네트워크 구성을 작성할 수도 있습니다. 





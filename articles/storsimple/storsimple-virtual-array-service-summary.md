---
title: StorSimple Virtual Array 서비스 요약 블레이드 | Microsoft Docs
description: StorSimple Device Manager에 대한 서비스 요약 블레이드 및 이 기능을 사용하여 StorSimple Virtual Array의 상태를 모니터링하는 방법을 설명합니다.
services: storsimple
documentationcenter: ''
author: manuaery
manager: syadav
editor: ''
ms.assetid: 8a2b9a84-b0e6-48b9-b366-d16f004241a5
ms.service: storsimple
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 31220a8f8b012e08d46195b60a26be9cfc261be5
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "85514519"
---
# <a name="use-the-service-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a>StorSimple 가상 배열에 연결된 StorSimple 디바이스 관리자에 대한 서비스 요약 블레이드 사용
## <a name="overview"></a>개요
StorSimple 디바이스 관리자에 대한 서비스 요약 블레이드는 서비스에 연결된 StorSimple 가상 배열(StorSimple 온-프레미스 가상 디바이스 또는 가상 디바이스라고도 함)에 대한 요약 보기를 제공하며 시스템 관리자의 주의가 필요한 정보를 강조하여 표시합니다. 이 자습서에서는 서비스 요약 블레이드를 소개하고, 콘텐츠와 기능 및 이 브레이드에서 수행할 수 있는 태스크에 대해 설명합니다.

![서비스 대시보드](./media/storsimple-virtual-array-service-summary/service-blade.png)

## <a name="management-commands-and-essentials"></a>관리 명령 및 Essentials
StorSimple 요약 블레이드에서 이 서비스에 등록된 가상 배열뿐만 아니라 StorSimple 디바이스 관리자 서비스를 관리하는 옵션이 표시됩니다. 블레이드 상단과 왼쪽에는 관리 명령이 표시됩니다.

이 옵션을 사용하여 공유 또는 볼륨을 추가하거나 가상 배열에서 실행 중인 다양한 작업을 모니터링하는 것과 같은 다양한 작업을 수행합니다.

Essentials 영역은 StorSimple 디바이스 관리자를 만든 리소스 그룹, 위치 및 구독과 같은 중요한 속성 중 일부를 캡처합니다.

## <a name="storsimple-device-manager-service-summary"></a>StorSimple 디바이스 관리자 서비스 요약
* **경고** 타일에서는 경고 심각도별로 그룹화된 모든 가상 디바이스 간의 모든 활성 경고에 대한 스냅샷을 제공합니다. 타일을 클릭하면 **경고** 블레이드가 열리고 여기에서 개별 경고를 클릭하여 권장 조치를 포함하여 해당 경고에 대한 추가적인 정보를 자세히 볼 수 있습니다. 또한 문제가 해결된 경고를 지울 수도 있습니다.
* **용량** 타일에서는 모든 가상 디바이스에서 사용 가능한 총 스토리지를 기준으로 모든 가상 디바이스에 프로비전하고 남아있는 기본 스토리지를 보여 줍니다. **프로비전** 은 사용하도록 준비되고 할당된 스토리지의 양을 나타내며 **나머지** 는 모든 가상 디바이스에 프로비전될 수 있는 남은 용량을 가리킵니다. **나머지 계층** 용량은 클라우드를 포함하여 프로비전될 수 있는 사용 가능한 용량인 반면 **나머지 로컬** 은 가상 배열에 연결된 디스크에 남아 있는 용량입니다.
* **사용량** 차트에서 가상 디바이스에 대한 관련 메트릭을 볼 수 있습니다. 기본 시간 간격인 지난 7일 동안 가상 디바이스에서 사용된 클라우드 스토리지는 물론, 모든 가상 디바이스에 걸쳐 사용되는 기본 스토리지도 볼 수 있습니다. 차트의 오른쪽 위 모서리에서 **편집** 옵션을 사용하여 다른 시간 단위를 선택합니다.
* **디바이스** 타일에서는 디바이스 상태별로 그룹화된 StorSimple 디바이스 관리자에서 가상 배열 수의 요약을 제공합니다. 이 타일을 클릭하여 **디바이스** 목록 블레이드를 연 다음 개별 디바이스를 클릭하여 디바이스에 특정된 디바이스 요약을 살펴봅니다. 또한 지정된 디바이스 요약 블레이드에서 디바이스 특정 작업을 수행할 수 있습니다. 디바이스 요약 블레이드에 대한 자세한 내용은 [디바이스 요약 블레이드](storsimple-virtual-array-device-summary.md)로 이동합니다.

## <a name="view-the-activity-logs"></a>작업 로그 보기
StorSimple 디바이스 관리자 내에서 수행된 다양한 작업을 보려면 StorSimple 서비스 요약 블레이드의 왼쪽에 있는 **작업 로그** 링크를 클릭합니다. 그러면 **작업 로그** 블레이드로 이동하여 최근에 수행한 작업의 요약을 볼 수 있습니다.

![활동 로그](./media/storsimple-virtual-array-service-summary/activity-log.png)

## <a name="next-steps"></a>다음 단계
로컬 웹 UI를 사용하여 [StorSimple 가상 배열을 관리](storsimple-ova-web-ui-admin.md)하는 방법을 알아봅니다.


---
title: StorSimple 가상 배열 업데이트 0.4 릴리스 정보| Microsoft Docs
description: 업데이트 0.4를 실행하는 StorSimple 가상 배열에 대한 중대한 미해결 문제 및 해결책을 설명합니다.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 392e930dcb69392b6f9425abba0efa516d5c82b8
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94967060"
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>StorSimple 가상 배열 업데이트 0.4 릴리스 정보

## <a name="overview"></a>개요

다음 릴리스 정보는 Microsoft Azure StorSimple 가상 배열 업데이트에 대한 중요한 미해결 문제 및 해결된 문제를 식별합니다.

릴리스 정보는 계속 업데이트되며, 해결 방법이 필요한 중대한 문제가 발견되면 해당 내용이 추가됩니다. StorSimple 가상 배열을 배포하기 전에 릴리스 정보에 포함된 정보를 주의 깊게 검토하세요.

업데이트 0.4는 소프트웨어 버전 **10.0.10289.0** 에 해당합니다.

> [!NOTE]
> 업데이트는 작업 중단 업데이트이며 디바이스를 다시 시작합니다. I/O가 진행 중인 경우 디바이스에 가동 중지 시간이 발생합니다.


## <a name="whats-new-in-the-update-04"></a>업데이트 0.4의 새로운 기능
업데이트 0.4는 주로 몇 가지 향상된 기능과 결합된 버그 수정 빌드입니다. 이 버전에서는 여러 가지 버그로 인해 이전 버전에서 발생했던 백업 오류가 해결되었습니다. 주요 향상된 기능 및 버그 수정은 다음과 같습니다.

- **Backup 성능 향상** - 이 릴리스는 백업 성능을 개선하기 위해 몇 가지 주요 향상된 기능을 만들었습니다. 그 결과 많은 수의 파일을 포함하는 백업은 전체 및 증분 백업에 대해 완료 시간에 상당한 감소를 보입니다.

- **향상된 복원 성능** - 이 릴리스는 많은 수의 파일을 사용하는 경우 복원 성능을 크게 개선하는 향상된 기능을 포함합니다. 2-4백만 개의 파일을 사용하는 경우 향상된 기능을 확인하기 위해 16GB RAM으로 가상 배열을 프로비전하는 것이 좋습니다. 2백만 개 미만의 파일을 사용하는 경우 가상 머신에 대한 최소 요구 사항은 계속해서 8GB RAM입니다.

- **지원 패키지에 대한 향상된 기능** - 향상된 기능은 지원 패키지로 디스크, CPU, 메모리, 네트워크 및 클라우드에 대한 통계의 로깅과 이로 인한 디바이스 문제의 진단/디버깅 프로세스 개선을 포함합니다.

- **로컬로 고정된 iSCSI 볼륨을 200GB로 제한** - 로컬로 고정된 볼륨의 경우 StorSimple 가상 배열에서 200GB iSCSI 볼륨으로 제한하는 것이 좋습니다. 계층화된 볼륨에 대한 로컬 예약은 프로비전된 볼륨 크기의 10%로 계속되지만 200GB로 제한됩니다. 

- **Backup 관련 버그 수정** - 이전 버전의 소프트웨어에서 백업 실패를 발생시키는 백업과 관련된 문제가 있었습니다. 이러한 버스는 이 릴리스에서 해결되었습니다.


## <a name="issues-fixed-in-the-update-04"></a>업데이트 0.4에서 해결된 문제

다음 표에서는 이 릴리스에서 수정된 문제를 간략하게 설명합니다.

| 아니요. | 기능 | 문제 |
| --- | --- | --- |
| 1 |Backup 성능|이전 릴리스에서 많은 수의 파일을 포함하는 백업은 완료하는 데 시간이 오래 걸렸습니다(대략 몇 일). 이 릴리스에서 전체 및 증분 백업은 완료 시간에 상당한 감소를 보입니다. |
| 2 |지원 패키지|디스크, CPU, 메모리, 네트워크 및 클라우드 통계는 이제 지원 로그에 기록되어 디바이스의 문제를 해결할 때 지원 패키지를 매우 효과적으로 개선합니다.|
| 3 |Backup |이전 릴리스에서 장기 실행 백업은 백업 오류를 일으키는 디바이스의 공간 부족을 발생시킬 수 있었습니다. 이 버그는 큐에 한 번에 5개 이하의 백업을 허용하여 이 릴리스에서 해결됩니다.|
| 4 |iSCSI | 이전 릴리스에서 계층화된 또는 로컬로 고정된 볼륨에 대한 로컬 예약은 프로비전된 볼륨 크기의 10%였습니다. 이 릴리스에서 로컬에 고정되어 있거나 계층화된 모든 iSCSI 볼륨에 대한 로컬 예약은 해당 볼륨 용량의 10%로 제한되며 최대값은 200GB(2TB를 초과하는 계층화된 볼륨의 경우)이므로, 로컬 디스크에서 공간이 더 많이 확보됩니다. 이 릴리스에서 로컬로 고정된 볼륨을 200GB로 제한하는 것이 좋습니다.|


## <a name="known-issues-in-the-update-04"></a>업데이트 0.4의 알려진 문제

다음 표에서는 이전 릴리스에서 언급된 문제 릴리스를 포함하여 StorSimple 가상 배열에 대해 알려진 문제를 간략하게 제공합니다. 

| 아니요. | 기능 | 문제 | 해결 방법/설명 |
| --- | --- | --- | --- |
| **1.** |업데이트 |미리 보기 릴리스에서 만든 가상 디바이스는 지원되는 일반 사용 가능 버전으로 업데이트될 수 없습니다. |이러한 가상 디바이스는 재해 복구(DR) 워크플로를 사용하여 일반 사용 가능 릴리스로 장애 조치되어야 합니다. |
| **2.** |프로비전된 데이터 디스크 |특정한 크기의 데이터 디스크를 프로비전하고 해당 StorSimple 가상 디바이스를 만들고 나면, 데이터 크기를 확장하거나 축소하지 말아야 합니다. 이를 시도하면 디바이스의 로컬 계층에서 모든 데이터가 손실됩니다. | |
| **3.** |그룹 정책 |디바이스가 도메인에 가입될 때 그룹 정책을 적용하면 디바이스 작업에 부정적인 영향이 있을 수 있습니다. |가상 배열이 Active Directory용 자체 OU(조직 구성 단위)에 있으며 GPO(그룹 정책 개체)가 적용되지 않았는지 확인합니다. |
| **4.** |로컬 웹 UI |Internet Explorer (IE ESC)에서 향상된 보안 기능이 활성화된 경우 문제 해결 또는 유지 관리와 같은 일부 로컬 웹 UI 페이지가 적절하게 작동하지 않을 수 있습니다. 해당 페이지의 단추도 작동하지 않을 수 있습니다. |Internet Explorer의 보안 강화 기능을 해제하십시오. |
| **5.** |로컬 웹 UI |Hyper-V 가상 머신에서 웹 UI의 네트워크 인터페이스는 10Gbps 인터페이스로 표시됩니다. |이러한 동작은 Hyper-V를 반영합니다. Hyper-V는 가상 네트워크 어댑터에 10Gbps를 항상 표시합니다. |
| **6.** |계층화된 볼륨 또는 공유 |StorSimple 계층화된 볼륨에서 애플리케이션에 대한 바이트 범위 잠금은 지원되지 않습니다. 바이트 범위 잠금을 사용하도록 설정하면 StorSimple 계층화가 실행되지 않습니다. |권장된 조치는 다음과 같습니다. <br></br>애플리케이션 논리에서 바이트 범위 잠금을 해제합니다.<br></br>계층화된 볼륨이 아니라 로컬로 고정된 볼륨에 이 애플리케이션에 대한 데이터를 배치하도록 선택합니다.<br></br>*주의*: 로컬로 고정된 볼륨을 사용하고 바이트 범위 잠금을 사용할 경우 복원이 완료되기 전에 로컬로 고정된 볼륨이 온라인 상태가 될 수 있습니다. 이러한 경우, 복원이 진행 중이면, 복원이 완료될 때까지 반드시 기다려야 합니다. |
| **7.** |계층화된 공유 |큰 파일로 작업하면 계층화가 매우 느려질 수 있습니다. |큰 파일을 사용하는 경우 가장 큰 파일이 공유 크기의 3% 보다 작은 것이 좋습니다. |
| **8.** |공유에 사용된 용량 |공유에 데이터가 없어도 공유 사용량이 표시될 수 있습니다. 이것은 공유에 사용된 용량에 메타데이터가 포함되기 때문입니다. | |
| **9.** |재해 복구 |파일 서버에 대한 재해 복구는 원본 디바이스의 도메인과 같은 도메인에만 수행할 수 있습니다. 다른 도메인의 대상 디바이스로 재해 복구는 이번 릴리스에서 지원되지 않습니다. |이후 릴리스에서 구현됩니다. |
| **5-10.** |Azure PowerShell |이번 릴리스에서는 Azure PowerShell을 통해 StorSimple 가상 디바이스를 관리할 수 없습니다. |가상 디바이스에 대한 모든 관리는 Azure 클래식 포털 및 로컬 웹 UI를 통해 수행됩니다. |
| **pt.** |암호 변경 |가상 배열 디바이스 콘솔은 EN-US 키보드 형식으로 입력하는 것을 허용합니다. | |
| **10.** |CHAP |CHAP 자격 증명은 일단 한 번 만들면 제거할 수 없습니다. 또한 CHAP 자격 증명을 수정하면 볼륨을 오프라인 상태로 만든 다음 온라인 상태로 변경해야 변경사항이 적용됩니다. |이 문제는 이후 릴리스에서 해결됩니다. |
| **/10.** |iSCSI 서버 |iSCSI 볼륨에 대해 표시된 '사용된 스토리지'는 StorSimple Manager 서비스 및 iSCSI 호스트에서 다를 수 있습니다. |iSCSI 호스트에는 파일 시스템 보기가 있습니다.<br></br>볼륨이 최대 크기일 때 디바이스에서는 블록이 할당된 것을 봅니다. |
| **14.** |파일 서버 |폴더의 파일에 연결된 ADS(대체 데이터 스트림)가 있는 경우 ADS는 재해 복구, 복제 및 항목 수준 복구를 통해 백업 또는 복원되지 않습니다. | |
| **15.** |파일 서버 |기호 링크는 지원되지 않습니다. | |
| **x.** |파일 서버 |Windows EFS(파일 시스템 암호화)에 의해 보호되는 파일을 StorSimple Virtual Array 파일 서버에 복사하거나 저장하지 마세요. 그러면 지원되지 않는 구성이 발생합니다.  | |

## <a name="next-step"></a>다음 단계
StorSimple 가상 배열에 [업데이트 0.4을 설치](storsimple-virtual-array-install-update-04.md) 합니다.

## <a name="references"></a>참조
이전 릴리스 정보를 찾으시나요? 다음으로 이동합니다. 

* [StorSimple 가상 배열 업데이트 0.3 릴리스 정보](storsimple-ova-update-03-release-notes.md)
* [StorSimple 가상 배열 업데이트 0.1 및 0.2 릴리스 정보](storsimple-ova-update-01-release-notes.md)
* [StorSimple 가상 배열 일반 공급 릴리스 정보](./storsimple-virtual-array-update-06-release-notes.md)
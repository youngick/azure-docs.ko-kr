---
title: StorSimple 10GbE 인터페이스에 대한 하드웨어 | Microsoft Docs
description: StorSimple 디바이스의 10GbE 네트워크 인터페이스에 대해 지원되는 SFP(Small Form Factor Pluggable) 트랜시버, 케이블 및 스위치에 대해 설명합니다.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: df8d40c7-f5ad-4f84-93eb-779fbd5f7243
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: fd30c7ec15eadd3d7945349a8aae4ac824bfdc7f
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94954089"
---
# <a name="supported-hardware-for-the-10-gbe-network-interfaces-on-your-storsimple-device"></a>StorSimple 디바이스의 10GbE 네트워크 인터페이스에 대해 지원되는 하드웨어

[!INCLUDE [storsimple-8000-eol-banner](../../includes/storsimple-8000-eol-banner.md)]

## <a name="overview"></a>개요
이 문서에서는 Microsoft Azure StorSimple 디바이스를 사용하는 보조 하드웨어에 대한 정보를 제공합니다.

## <a name="list-of-devices-tested-by-microsoft"></a>Microsoft에서 테스트한 디바이스 목록
Microsoft는 다음과 같은 소형 폼팩터 플러그형(SFP) 트랜시버, 케이블 및 스위치가 디바이스와 최적으로 작동되도록 테스트했습니다. (새 하드웨어를 테스트하는 대로 다음 표가 업데이트됩니다.)

### <a name="sfp-transceivers"></a>SFP + 트랜시버
| Make | 모델 |
| --- | --- |
| 시스코 |SFP-10G-SR |

### <a name="cables"></a>케이블
| S.는 아니요. | Make | 모델 |
| --- | --- | --- |
| 1. |시스코 |SFP-H10GB-CU1M |
| 2. |시스코 |SFP-H10GB-CU2M |
| 3. |시스코 |SFP-H10GB-CU3M |
| 4. |Tripp-Lite |N820-05M (OM3) |

### <a name="switches"></a>스위치
| S.는 아니요. | Make | 모델 |
| --- | --- | --- |
| 1. |시스코 |N3K-C3172PQ-10GE |
| 2. |시스코 |N3K-C3048-ZM-F |
| 3. |시스코 |N5K-C5596UP-FA |

## <a name="list-of-devices-tested-in-the-field"></a>필드에서 테스트한 디바이스 목록
이 섹션에는 StorSimple 고객이 필드에 성공적으로 배포한 디바이스 목록이 포함되어 있습니다. Microsoft에서 테스트하지 않았지만 StorSimple 디바이스와 작업할 수 있습니다.

| 매개 변수 | 값 |
| --- | --- |
| 스위치 제조사 |Juniper |
| 스위치 모델 |ex4550-32F |
| 스위치 운영 체제 버전 |JunOS 12.3R9.4 |
| 블레이드 모델 |포트 등록(PIC 0) |
| 송수신 장치 제조사 |Juniper |
| 송수신 장치 모델 |부품 번호 740-021308 <br></br>  부품 번호 740-030658 |
| 송수신 장치 펌웨어 버전 |Rev 01 버전 0.0(보고됨) |
| 케이블 모델 |이중 점퍼 LC/LC 50/125μ, OM3, LSZH |
| StorSimple 모델 |8600 |
| StorSimple 소프트웨어 버전 |6.3.9600.17491 |

## <a name="list-of-devices-tested-by-oem-provider-mellanox"></a>OEM 공급자(Mellanox)가 테스트한 디바이스 목록
다음 소형 폼팩터 플러그형(SFP) 트랜시버, 케이블 및 스위치는 StorSimple 디바이스의 10GbE 네트워크 인터페이스와 같은 Mellanox 네트워크 인터페이스와 최적으로 작동되도록 Mellanox에서 테스트되었습니다.

### <a name="cables-and-modules-supported-by-mellanox"></a>Mellanox에서 지원하는 케이블 및 모듈
다음 표에서 Mellanox에서 지 원하는 케이블 및 모듈을 나열합니다. Microsoft에서 테스트하지 않았지만 StorSimple 디바이스와 작업할 수 있습니다.

| S.는 아니요. | 속도 | 모델 | 설명 | Make |
| --- | --- | --- | --- | --- |
| 1. |10GbE |CAB-SFP-SFP-1M |수동 구리 케이블 SFP+10Gb/s 1m |Arista |
| 2. |10GbE |CAB-SFP-SFP-2M |수동 구리 케이블 SFP+10Gb/s 2m |Arista |
| 3. |10GbE |CAB-SFP-SFP-3M |수동 구리 케이블 SFP+10Gb/s 3m |Arista |
| 4. |10GbE |CAB-SFP-SFP-5M |수동 구리 케이블 SFP+10Gb/s 5m |Arista |
| 5. |10GbE |Cisco SFP-H10GBCU1M |Cisco SFP+ 케이블 |시스코 |
| 6. |10GbE |Cisco SFP-H10GBCU3M |Cisco SFP+ 케이블 |시스코 |
| 7. |10GbE |Cisco SFP-H10GBCU5M |Cisco SFP+ 케이블 |시스코 |
| 8. |10GbE |J9281B HP X242 10G |SFP + SFP + 1m 구리 케이블 연결 |HP |
| 9. |10GbE |455883-B21 HP BLc |10Gb SR SFP+ Opt |HP |
| 10. |10GbE |455886-B21 HP BLc |10Gb LR SFP+ Opt |HP |
| 11. |10GbE |487649-B21 HP BLc |SFP + 0.5m 10GbE 구리 케이블 |HP |
| 12. |10GbE |487652-B21 HP BLc |SFP + 1m 10GbE 구리 케이블 |HP |
| 13. |10GbE |487655-B21 HP BLc |SFP + 3m 10GbE 구리 케이블 |HP |
| 14. |10GbE |487658-B21 HP BLc |SFP + 7m 10GbE 구리 케이블 |HP |
| 15. |10GbE |537963-B21 HP BLc |SFP + 5m 10GbE 구리 케이블 |HP |
| 16. |10GbE |AP784A HP |3m C 시리즈 수동 구리 SFP + 케이블 |HP |
| 17. |10GbE |AP785A HP |5m C 시리즈 수동 구리 SFP + 케이블 |HP |
| 18. |10GbE |AP818A HP |1m B 시리즈 활성 구리 SFP + 케이블 |HP |
| 19. |10GbE |AP819A HP |3m B 시리즈 활성 구리 SFP + 케이블 |HP |
| 20. |10GbE |J9150A HP |X132 10G SFP+ LC SR 트랜시버 |HP |
| 21. |10GbE |J9151A HP |X132 10G SFP+ LC LR 트랜시버 |HP |
| 22. |10GbE |J9283B HP |X242 10G SFP + SFP + 3m DAC 케이블 |HP |
| 23. |10GbE |J9285B HP |X242 10G SFP + SFP + 7m DAC 케이블 |HP |
| 24. |10GbE |JD095B HP |X240 10G SFP+ SFP+ 0.65m DAC 케이블 |HP |
| 25. |10GbE |JD096B HP |X240 10G SFP+ SFP+ 1.2m DAC 케이블 |HP |
| 26. |10GbE |JD097B HP |X240 10G SFP+ SFP+ 3m DAD 케이블 |HP |
| 27. |10GbE |MAM1Q00A-QSA Mellanox |QSFP To SFP+ 어댑터 |Mellanox 기술 |
| 28. |10GbE |MC2309124-006 Mt |수동 구리 케이블 1x SFP + To QSFP 10Gb/s 24awg 7m |Mellanox 기술 |
| 29. |10GbE |MC2309124-007 Mt |수동 구리 케이블 1x SFP + To QSFP 10Gb/s 24awg 7m |Mellanox 기술 |
| 30. |10GbE |MC2309130-003 Mt |수동 구리 케이블 1x SFP + To QSFP 10Gb/s 30awg 3m |Mellanox 기술 |
| 31. |10GbE |MC2309130-00A Mt |수동 구리 케이블 1x SFP + To QSFP 10Gb/s 30awg 0.5m |Mellanox 기술 |
| 32. |10GbE |MC3309124-005 Mt |수동 구리 케이블 1x SFP + 10Gb/s 24awg 5m |Mellanox 기술 |
| 33. |10GbE |MC3309124-007 Mt |수동 구리 케이블 1x SFP + 10Gb/s 24awg 7m |Mellanox 기술 |
| 34. |10GbE |MC3309130-003 Mt |수동 구리 케이블 1x SFP + 10Gb/s 30awg 3m |Mellanox 기술 |
| 35. |10GbE |MC3309130-00A Mt |수동 구리 케이블 1x SFP + 10Gb/s 30awg 0.5m |Mellanox 기술 |

### <a name="switches-supported-by-mellanox"></a>Mellanox에서 지원하는 스위치
다음 표는 Mellanox에서 지원하는 스위치를 나열합니다. Microsoft에서 테스트하지 않았지만 StorSimple 디바이스와 작업할 수 있습니다.

| S.는 아니요. | 속도 | 모델 | 설명 | Make |
| --- | --- | --- | --- | --- |
| 1. |10GbE |516733-B21 |HP ProCurve 6120XG 10GbE 이더넷 블레이드 스위치 |HP |
| 2. |10GbE |538113-B21 |HP 10GbE 통과 모듈(PTM) |HP |
| 3. |10GbE |EN4093 |IBM PureFlex System Fabric EN4093 10기가비트 확장성 있는 스위치 모듈 |IBM |
| 4. |1GbE |3020 |Cisco Catalyst 3020 1GbE 스위치 블레이드 |시스코 |
| 5. |1GbE |3020X |Cisco Catalyst 3020X 1GbE 스위치 블레이드 |시스코 |
| 6. |1GbE |438030-B21 |HP 1GbE 스위치 모듈 - GbE2c 계층 2/3 이더넷 블레이드 전환 |HP |
| 7. |1GbE |6120G |HP ProCurve 6120G/XG 1GbE 스위치 블레이드 |HP |

## <a name="next-steps"></a>다음 단계
[StorSimple 하드웨어 구성 요소 및 상태에 대해 자세히 알아보기](./storsimple-8000-monitor-hardware-status.md)
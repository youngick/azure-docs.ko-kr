---
title: Azure Percept DK 구성 요소 언박싱 및 조립
description: Azure Percept DK를 언박싱 및 연결하고 기능을 활용하는 방법에 대해 알아봅니다.
author: elqu20
ms.author: v-elqu
ms.service: azure-percept
ms.topic: quickstart
ms.date: 02/16/2021
ms.custom: template-quickstart
ms.openlocfilehash: 40751401760d877fe3feab39f3fea1f2fbeee54b
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2021
ms.locfileid: "101664297"
---
# <a name="quickstart-unbox-and-assemble-your-azure-percept-dk-components"></a>빠른 시작: Azure Percept DK 구성 요소 언박싱 및 조립

Azure Percept DK를 받은 후에는 이 가이드에서 구성 요소를 연결하고 디바이스를 켜는 방법에 대한 정보를 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

- Azure Percept DK(Devkit)
- P7 드라이버(선택 사항, 캐리어 보드에 전원 케이블 커넥터를 고정하는 데 사용)

## <a name="unbox-and-assemble-your-device"></a>디바이스 언박싱 및 조립

1. Azure Percept DK 구성 요소를 언박싱합니다.

    Devkit에는 캐리어 보드, Azure Percept Vision SoM, 안테나와 케이블이 있는 액세서리 상자, 육각 키가 있는 환영 카드가 포함되어 있습니다.

1. Devkit 구성 요소를 연결합니다.

    > [!NOTE]
    > 전원 어댑터 포트는 캐리어 보드의 오른쪽에 있습니다. 나머지 포트(USB-A 2개, USB-C 1개, HDMI 1개 및 이더넷 1개)와 리셋 단추는 캐리어 보드의 왼쪽에 있습니다.

    1. Wi-Fi 안테나를 캐리어 보드에 나사로 고정합니다.

    1. USB-C 케이블을 사용하여 캐리어 보드의 USB-C 포트에 Vision SoM을 연결합니다.

    1. 전원 어댑터에 전원 케이블을 연결합니다.

    1. 나머지 플라스틱 패키징을 디바이스에서 제거합니다.

    1. 전원 어댑터/케이블을 캐리어 보드와 벽 콘센트에 연결합니다. 전원 케이블 커넥터를 캐리어 보드에 단단히 고정하기 위해 P7 드라이버(Devkit에 미포함)를 사용하여 커넥터 나사를 조입니다.

    1. 벽 콘센트에 전원 케이블을 연결하면 디바이스가 자동으로 켜집니다. 캐리어 보드의 왼쪽에 있는 리셋 단추가 점등됩니다. 디바이스를 부팅하는 데는 어느 정도 시간이 걸릴 수 있습니다.

        > [!NOTE]
        > 리셋 단추는 전원 콘센트에 연결된 상태에서 디바이스의 전원을 끄거나 초기화할 때 사용할 수 있습니다. 정전 시에는 디바이스가 자동으로 초기화되고 전원이 켜집니다.

## <a name="next-steps"></a>다음 단계

이제 Devkit가 연결되고 전원이 켜졌으므로 Azure Percept DK 설정 환경 연습을 참조하여 디바이스 설정을 완료하세요. 설정 환경에서는 Devkit를 Wi-Fi 네트워크에 연결하고, SSH 로그인을 설정하고, IoT Hub를 만들고, Devkit를 Azure 계정에 프로비저닝할 수 있습니다. 디바이스 설정을 완료하면 프로토타입 생성을 시작할 준비가 된 것입니다.
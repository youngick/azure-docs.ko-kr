---
author: dominicbetts
ms.author: dominicbetts
ms.service: iot-pnp
ms.topic: include
ms.date: 11/15/2019
ms.openlocfilehash: 647226091c3e15a19bf8262c23e62d95018488b3
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99831209"
---
IoT 플러그 앤 플레이 추가 문서를 계속 진행하려는 경우 이 문서에서 사용한 리소스를 유지하고 재사용할 수 있습니다. 그렇지 않으면 이 문서에서 만든 리소스를 삭제하여 추가 요금을 방지할 수 있습니다.

다음 Azure CLI 명령을 사용하여 전체 리소스 그룹을 삭제하면 허브와 등록된 디바이스를 한 번에 삭제할 수 있습니다. 이러한 리소스가 유지하려는 다른 리소스와 리소스 그룹을 공유하는 경우에는 이 명령을 사용하지 마세요.

```azurecli-interactive
az group delete --name <YourResourceGroupName>
```

IoT 허브만 삭제하려면 Azure CLI을 사용하여 다음 명령을 실행합니다.

```azurecli-interactive
az iot hub delete --name <YourIoTHubName>
```

IoT 허브에 등록한 디바이스 ID만 삭제하려면 Azure CLI를 사용하여 다음 명령을 실행합니다.

```azurecli-interactive
az iot hub device-identity delete --hub-name <YourIoTHubName> --device-id <YourDeviceID>
```

개발 머신에서 복제된 샘플 파일을 제거할 수도 있습니다.

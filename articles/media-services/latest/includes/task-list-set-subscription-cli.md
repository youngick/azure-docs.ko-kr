---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 08/17/2020
ms.author: inhenkel
ms.custom: CLI
ms.openlocfilehash: aa76f7b85302651f6874747610c3355f0572a7ee
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94885444"
---
<!-- List and set subscriptions -->

1. [az account list](/cli/azure/account#az-account-list) 명령을 사용하여 구독 리스트를 가져옵니다.

    ```
    az account list --output table
    ```

2. 전환하려고 하는 구독 ID 또는 이름으로 `az account set`을 사용합니다.

    ```
    az account set --subscription "My Demos"
    ```

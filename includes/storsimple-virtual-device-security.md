---
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 10/26/2018
ms.author: alkohli
ms.openlocfilehash: cb160a140b5c0cb184a5172da10ade0de37c4fed
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "67182247"
---
<!--v-sharos 10/13/2105 virtual device security-->

StorSimple 가상 디바이스를 사용하는 경우 다음 보안 고려 사항을 염두에 두세요.

* 가상 디바이스는 Microsoft Azure 구독을 통해 보안이 설정됩니다. 가상 디바이스를 사용하고 Azure 구독이 손상되는 경우, 가상 디바이스에 저장된 데이터도 노출되기 쉬움을 의미합니다.
* Azure StorSimple에 저장된 데이터를 암호화하는 데 사용되는 인증서의 공개 키는 Azure 클래식 포털에서 안전하게 사용할 수 있으며 프라이빗 키는 StorSimple 디바이스에 유지됩니다. StorSimple 가상 디바이스에서 공개 및 프라이빗 키는 모두 Azure에 저장됩니다.
* 가상 디바이스는 Microsoft Azure 데이터 센터에서 호스팅됩니다.


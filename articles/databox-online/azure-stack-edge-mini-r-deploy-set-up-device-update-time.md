---
title: Azure Portal에서 Azure Stack Edge Mini R 디바이스에 대한 디바이스, 업데이트, 시간을 설정하는 자습서 | Microsoft Docs
description: Azure Stack Edge Mini R을 배포하기 위한 자습서에서는 물리적 디바이스에 대한 디바이스, 업데이트 및 시간 설정을 설정하는 방법을 안내합니다.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 10/14/2020
ms.author: alkohli
Customer intent: As an IT admin, I need to understand how to connect and activate Azure Stack Edge Mini R  so I can use it to transfer data to Azure.
ms.openlocfilehash: e9f4d4f4ad27081bb105cdb1698438837fc2fe02
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "100546672"
---
# <a name="tutorial-configure-the-device-settings-for-azure-stack-edge-mini-r"></a>자습서: Azure Stack Edge Mini R에 대한 디바이스 설정 구성

이 자습서에서는 온보드 GPU가 있는 Azure Stack Edge Mini R 디바이스에 대한 디바이스 관련 설정을 구성하는 방법을 설명합니다. 로컬 웹 UI를 통해 디바이스 이름, 업데이트 서버 및 시간 서버를 설정할 수 있습니다.

디바이스 설정을 완료하는 데 약 5~7분이 걸릴 수 있습니다.

이 자습서에서는 다음에 대해 알아봅니다.

> [!div class="checklist"]
>
> * 필수 조건
> * 디바이스 설정 구성
> * 업데이트 구성 
> * 시간 구성

## <a name="prerequisites"></a>필수 조건

GPU가 있는 Azure Stack Edge Mini R 디바이스에서 디바이스 관련 설정을 구성하기 전에 다음 사항을 확인합니다.

* 물리적 디바이스:

    - [Azure Stack Edge Mini R 설치](azure-stack-edge-mini-r-deploy-install.md)에서 설명한 대로 물리적 디바이스를 설치했습니다.
    - [자습서: GPU가 있는 Azure Stack Edge Mini R에 대한 네트워크 구성](azure-stack-edge-mini-r-deploy-configure-network-compute-web-proxy.md)에 자세히 설명된 대로 디바이스에서 네트워크를 구성하고 컴퓨팅 네트워크를 사용하도록 설정하고 구성했습니다.


## <a name="configure-device-settings"></a>디바이스 설정 구성

디바이스 관련 설정을 구성하려면 다음 단계를 수행합니다.

1. **디바이스** 페이지에서 다음 단계를 수행합니다.

    1. 디바이스의 식별 이름을 입력합니다. 식별 이름은 1~13자로 구성되어야 하며 문자, 숫자 및 하이픈을 포함할 수 있습니다.

    2. 디바이스의 **DNS 도메인** 을 지정합니다. 이 도메인은 디바이스를 파일 서버로 설정하는 데 사용됩니다.

    3. 구성된 디바이스 설정의 유효성을 검사하고 설정을 적용하려면 **적용** 을 선택합니다.

        ![로컬 웹 UI "디바이스" 페이지 1](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/set-up-device-1.png)

        디바이스 이름과 DNS 도메인을 변경한 경우에는 디바이스에 있는 자체 서명된 인증서가 작동하지 않습니다. 

        ![로컬 웹 UI "디바이스" 페이지 2](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/set-up-device-2.png)

        인증서를 구성할 때 다음 옵션 중 하나를 선택해야 합니다. 
        
        - 디바이스 인증서를 생성하고 다운로드합니다. 
        - 서명 체인을 포함한 디바이스의 자체 인증서를 가져옵니다.
    

    4. 디바이스 이름 및 DNS 도메인이 변경되면 SMB 엔드포인트가 생성됩니다.  

        ![로컬 웹 UI "디바이스" 페이지 3](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/set-up-device-3.png)

    5. 설정이 적용된 후 **다음: 업데이트 서버** 를 선택합니다.


## <a name="configure-update"></a>업데이트 구성

1. 이제 **업데이트** 페이지에서 디바이스에 대한 업데이트를 다운로드할 위치를 구성할 수 있습니다.  

    - **Microsoft 업데이트 서버** 에서 직접 업데이트를 가져올 수 있습니다.

        ![로컬 웹 UI "업데이트 서버" 페이지](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/update-server-1.png)

        WSUS(**Windows Server Update services**)에서 업데이트를 배포하도록 선택할 수도 있습니다. WSUS 서버의 경로를 지정합니다.
        
        ![로컬 웹 UI "업데이트 서버" 페이지 2](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/update-server-2.png)

        > [!NOTE] 
        > 별도의 Windows 업데이트 서버가 구성되어 있고 *http* 가 아닌 *https* 를 통해 연결하도록 선택한 경우 업데이트 서버에 연결하는 데 필요한 서명 체인 인증서가 있어야 합니다. 인증서를 만들고 업로드하는 방법에 대한 자세한 내용은 [인증서 관리](azure-stack-edge-gpu-manage-certificates.md)를 참조하세요. 모듈식 데이터 센터에 대한 Azure Stack Edge 디바이스 계층과 같은 연결 끊김 모드에서 작업하려면 WSUS 옵션을 사용하도록 설정합니다. 활성화하는 동안 디바이스에서 업데이트를 검색하고, 서버가 설정되지 않은 경우 활성화가 실패합니다. 

2. **적용** 을 선택합니다.
3. 업데이트 서버가 구성되었으면 **다음: 시간** 을 선택합니다.
    

## <a name="configure-time"></a>시간 구성

다음 단계에 따라 디바이스에 대한 시간 설정을 구성합니다. 

> [!IMPORTANT]
> 시간 설정은 선택 사항이지만 디바이스의 로컬 네트워크에 기본 NTP 및 보조 NTP 서버를 구성할 것을 적극 권장합니다. 로컬 서버를 사용할 수 없는 경우 공용 NTP 서버를 구성할 수 있습니다.

클라우드 서비스 공급자와 인증할 수 있도록 디바이스 시간을 동기화해야 하기 때문에 NTP 서버가 필요합니다.

1. **시간** 페이지에서 디바이스의 표준 시간대와 기본 및 보조 NTP 서버를 선택할 수 있습니다.  
    
    1. **표준 시간대** 드롭다운 목록에서 해당 디바이스가 배포되는 지리적 위치에 해당하는 표준 시간대를 선택합니다.
        디바이스의 기본 표준 시간대는 PST입니다. 디바이스는 모든 예약된 작업에 대해 이 표준 시간대를 사용합니다.

    2. **기본 NTP 서버** 상자에 디바이스의 주 서버를 입력하거나 기본값인 time.windows.com을 그대로 적용합니다.  
        네트워크에서 NTP 트래픽이 데이터 센터에서 인터넷으로 전달되도록 허용하는지 확인합니다.

    3. 필요에 따라 **보조 NTP 서버** 상자에 디바이스의 보조 서버를 입력합니다.

    4. 구성된 시간 설정의 유효성을 검사하고 설정을 적용하려면 **적용** 을 선택합니다.

        ![로컬 웹 UI "시간" 페이지](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/time-settings-1.png)

2. 설정이 적용된 후 **다음: 인증서** 를 선택합니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음에 대해 알아봅니다.

> [!div class="checklist"]
>
> * 필수 조건
> * 디바이스 설정 구성
> * 업데이트 구성 
> * 시간 구성

Azure Stack Edge Mini R 디바이스의 인증서를 구성하는 방법을 알아보려면 다음을 참조하세요.

> [!div class="nextstepaction"]
> [인증서 구성](./azure-stack-edge-mini-r-deploy-configure-certificates-vpn-encryption.md)

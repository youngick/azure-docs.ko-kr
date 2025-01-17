---
title: 파일 포함
description: 포함 파일
services: site-recovery
author: mayurigupta13
manager: rochakm
ms.service: site-recovery
ms.topic: include
ms.date: 02/28/2019
ms.author: mayg
ms.custom: include file
ms.openlocfilehash: f699ffe6d5a91e8ce3ae90c7e12249bbad0fff3e
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96001565"
---
1. 통합 설치 프로그램 설치 파일을 실행합니다.
2. **시작하기 전에** 에서 **구성 서버 및 프로세스 서버 설치** 를 선택합니다.

    ![통합 설치 프로그램의 시작하기 전 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. **타사 소프트웨어 라이선스** 에서 **동의함** 을 클릭하고 MySQL을 다운로드 및 설치합니다.

    ![통합 설치 프로그램의 타사 소프트웨어 라이선스 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. **등록** 에서 자격 증명 모음에서 다운로드한 등록 키를 선택합니다.

    ![통합 설치 프로그램의 등록 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. **인터넷 설정** 에서 구성 서버에서 실행 중인 공급자가 인터넷을 통해 Azure Site Recovery에 연결하는 방법을 지정합니다. 필수 URL을 허용했는지 확인합니다.

    - 현재 컴퓨터에 설정된 프록시를 사용하여 연결하려면 **프록시 서버를 사용하여 Azure Site Recovery에 연결** 을 선택합니다.
    - 공급자를 직접 연결하려면 **프록시 서버 없이 Azure Site Recovery에 직접 연결** 을 선택합니다.
    - 기존 프록시에 인증이 필요하거나 공급자 연결에 사용자 지정 프록시를 사용하려면 **사용자 지정 프록시 설정으로 연결** 을 선택하고 주소, 포트 및 자격 증명을 지정합니다.
     ![통합 설치 프로그램의 인터넷 설정 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. **필수 조건 확인** 에서 설치 프로그램은 설치가 실행될 수 있는지 확인합니다. **글로벌 시간 동기화 확인** 에 대한 경고가 표시되면 시스템 시계의 시간(**날짜 및 시간** 설정)이 표준 시간대와 같은지 확인합니다.

    ![통합 설치 프로그램의 필수 구성 요소 확인 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. **MySQL 구성** 에서 설치된 MySQL 서버 인스턴스에 로그온하기 위한 자격 증명을 만듭니다.

    ![통합 설치 프로그램의 MySQL 구성 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. Azure Stack VM 또는 실제 서버를 복제하는 경우 **환경 세부 정보** 에서 [아니요]를 선택합니다. 
9. **설치 위치** 에서 이진 파일을 설치하고 캐시를 저장할 위치를 선택합니다. 최소 5GB의 디스크 공간이 있는 드라이브를 선택해야 하지만 600GB 이상의 사용 가능한 공간이 있는 캐시 드라이브를 선택하는 것이 좋습니다.

    ![통합 설치 프로그램의 설치 위치 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. **네트워크 선택** 에서 먼저 기본 제공 프로세스 서버가 원본 머신에서 Mobility Service의 검색 및 푸시 설치에 사용하는 NIC를 선택한 다음, 구성 서버에서 Azure와의 연결에 사용하는 NIC를 선택합니다. 9443 포트는 복제 트래픽을 보내고 받는 데 사용되는 기본 포트이지만, 환경의 요구 사항에 맞게 이 포트 번호를 수정할 수 있습니다. 9443 포트 외에도 웹 서버에서 복제 작업을 조정하기 위해 사용하는 443 포트를 엽니다. 복제 트래픽을 보내거나 받는 데 443 포트를 사용하면 안 됩니다.

    ![통합 설치 프로그램의 네트워크 선택 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. **요약** 에서 정보를 검토하고 **설치** 를 클릭합니다. 설치가 완료되면 암호가 생성됩니다. 복제를 사용하도록 설정할 때 필요하므로 암호를 복사하고 안전한 위치에 보관합니다.

    ![통합 설치 프로그램의 요약 화면에 대한 스크린샷](./media/site-recovery-add-configuration-server/combined-wiz10.png)

등록이 완료되면 자격 증명 모음의 **설정** > **서버** 블레이드에 서버가 표시됩니다.

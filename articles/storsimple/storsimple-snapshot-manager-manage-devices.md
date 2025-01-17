---
title: StorSimple Snapshot Manager에서 디바이스 관리 | Microsoft Docs
description: StorSimple 스냅샷 관리자 MMC 스냅인을 사용하여 StorSimple 디바이스를 연결하고 관리하는 방법을 설명합니다.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: how-to
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: dbb7e835d110bcb6cb81fd5425a2aafbb578e692
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96022975"
---
# <a name="use-storsimple-snapshot-manager-to-connect-and-manage-storsimple-devices"></a>StorSimple Snapshot Manager를 사용하여 StorSimple 디바이스 연결 및 관리
## <a name="overview"></a>개요
StorSimple Snapshot Manager의 **범위** 창에서 노드를 사용하여 가져온 StorSimple 디바이스 데이터를 확인하고 연결된 스토리지 디바이스를 새로 고칠 수 있습니다. 또한, **장치** 노드를 클릭하면 **결과** 창에서 연결된 장치 목록과 해당 상태 정보를 볼 수 있습니다.

![연결된 디바이스](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**그림 1: StorSimple Snapshot Manager 연결된 디바이스** 

**뷰** 선택 항목에 따라 **결과** 창에 각 장치에 대해 다음과 같은 정보를 표시합니다. (보기 구성에 대한 자세한 내용은 [보기 메뉴](storsimple-use-snapshot-manager.md#view-menu)를 참조하세요.)

| 결과 열 | 설명 |
|:--- |:--- |
| Name |디바이스의 이름은 Azure 클래식 포털에서 구성된 이름을 따릅니다. |
| 모델 |디바이스의 모델 번호 |
| 버전 |디바이스에 설치된 소프트웨어 버전 |
| 상태 |디바이스를 사용할 수 있는지 여부 |
| 마지막 동기화 |디바이스를 마지막으로 동기화한 날짜 및 시간 |
| 일련 번호 |디바이스의 일련 번호 |

**범위** 창에서 **장치** 노드를 마우스 오른쪽 단추로 클릭하면 다음 작업 중에서 선택할 수 있습니다.

* 디바이스 추가 또는 교체
* 디바이스 연결 및 가져오기 확인
* 연결된 디바이스 새로 고침

**장치** 노드를 클릭하고 **결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭하면 다음 작업 중에서 선택할 수 있습니다.

* 디바이스 인증
* 디바이스 세부 정보 보기
* 디바이스 새로 고침
* 디바이스 구성 삭제
* 디바이스 암호 변경

> [!NOTE]
> 이러한 모든 작업은 **작업** 창에서도 사용할 수 있습니다.


이 자습서에서는 StorSimple 스냅샷 관리자를 사용하여 디바이스를 연결 및 관리하고 다음 작업을 수행하는 방법에 대해 설명합니다.

* 디바이스 추가 또는 교체
* 디바이스 연결 및 가져오기 확인
* 연결된 디바이스 새로 고침
* 디바이스 인증
* 디바이스 세부 정보 보기
* 개별 디바이스 새로 고침
* 디바이스 구성 삭제
* 만료된 디바이스 암호 변경
* 실패한 디바이스 바꾸기

> [!NOTE]
> StorSimple 스냅샷 관리자 인터페이스 사용에 대한 일반적인 정보는 [StorSimple 스냅샷 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)를 참조하세요.


## <a name="add-or-replace-a-device"></a>디바이스 추가 또는 교체
다음 절차에 따라 StorSimple 디바이스를 추가하거나 교체할 수 있습니다.

#### <a name="to-add-or-replace-a-device"></a>디바이스를 추가 또는 교체하려면
1. 바탕 화면 아이콘을 클릭하여 StorSimple 스냅샷 관리자를 시작합니다.
2. **범위** 창에서 **장치** 노드를 마우스 오른쪽 단추로 클릭한 다음 **장치 구성** 을 클릭합니다. **장치 구성** 대화 상자가 나타납니다.
   
    ![StorSimple 디바이스 구성](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. **디바이스** 드롭다운 상자에서 디바이스 또는 가상 디바이스의 IP 주소를 선택합니다. 
4. **암호** 텍스트 상자에 Azure 클래식 포털에서 디바이스에 대해 만든 StorSimple Snapshot Manager 암호를 입력합니다. **확인** 을 클릭합니다. StorSimple 스냅샷 관리자에서 사용자가 지정한 디바이스를 검색합니다. 
   
   * 디바이스를 사용할 수 있으면 StorSimple Snapshot Manager가 연결을 추가합니다.
   * 어떤 이유로든 디바이스를 사용할 수 없으면 StorSimple 스냅샷 관리자에서 오류 메시지를 반환합니다. **확인** 을 클릭해 오류 메시지를 닫고 **취소** 를 클릭해 **장치 구성** 대화 상자를 닫습니다.

## <a name="connect-a-device-and-verify-imports"></a>디바이스 연결 및 가져오기 확인
다음 절차에 따라 StorSimple 디바이스를 연결하고 연결된 백업이 있는 모든 기존 볼륨 그룹을 가져왔는지 확인할 수 있습니다.

#### <a name="to-connect-a-device-and-verify-imports"></a>디바이스를 연결하고 가져오기를 확인하려면
1. StorSimple 스냅샷 관리자에 디바이스를 연결하려면 디바이스 추가 또는 교체에 나온 지침을 따릅니다. 디바이스에 연결되면 StorSimple 스냅샷 관리자가 다음과 같이 응답합니다.
   
   * 어떤 이유로든 디바이스를 사용할 수 없으면 StorSimple 스냅샷 관리자에서 오류 메시지를 반환합니다. 
   
   * 디바이스를 사용할 수 있으면 StorSimple Snapshot Manager가 연결을 추가합니다. 장치를 선택하면 장치가 **결과** 창에 나타나고 상태 필드는 장치를 **사용 가능** 으로 나타냅니다. 볼륨 그룹에 연결된 백업이 있는 경우 StorSimple 스냅샷 관리자는 해당 디바이스에 대해 구성된 모든 볼륨 그룹을 가져옵니다. Backup 정책은 가져오지 않습니다. 연결된 백업이 없는 볼륨 그룹은 가져오지 않습니다.
2. 바탕 화면 아이콘을 클릭하여 StorSimple 스냅샷 관리자를 시작합니다.
3. **범위** 창의 최상단 노드를 마우스 오른쪽 단추로 클릭한 다음 **가져오기 표시 전환** 을 클릭합니다.
   
    ![가져오기 표시 토글 선택](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. **가져오기 표시 전환** 대화 상자가 나타나 가져온 볼륨 그룹 및 백업 상태를 표시합니다. **확인** 을 클릭합니다.

볼륨 그룹과 백업을 성공적으로 가져온 후에는 StorSimple 스냅샷 관리자로 만들고 구성한 볼륨 그룹과 백업을 관리하는 것과 마찬가지로 StorSimple 스냅샷 관리자를 사용하여 관리할 수 있습니다. 

## <a name="refresh-connected-devices"></a>연결된 디바이스 새로 고침
다음 절차에 따라 연결된 StorSimple 디바이스를 StorSimple 스냅샷 관리자와 동기화할 수 있습니다.

#### <a name="to-refresh-connected-devices"></a>연결된 디바이스를 새로 고치려면
1. 바탕 화면 아이콘을 클릭하여 StorSimple 스냅샷 관리자를 시작합니다.
2. **범위** 창에서 **장치** 를 마우스 오른쪽 단추로 클릭하고 **장치 새로 고침** 을 클릭합니다. 그러면 연결된 디바이스와 StorSimple Snapshot Manager가 동기화되어 최근에 추가된 모든 항목을 비롯한 볼륨 그룹 및 백업을 볼 수 있습니다. 
   
    ![StorSimple 디바이스 새로 고침](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

**장치 새로 고침** 작업은 연결된 장치에서 새 볼륨 그룹과 그와 연결된 모든 백업을 검색합니다. **볼륨** 노드에서 사용할 수 있는 **볼륨 다시 검사** 작업과 달리 **디바이스 새로 고침** 은 백업 레지스트리를 복원하지 않습니다.

## <a name="authenticate-a-device"></a>디바이스 인증
다음 절차에 따라 StorSimple 스냅샷 관리자에서 StorSimple 디바이스를 인증할 수 있습니다.

#### <a name="to-authenticate-a-device"></a>디바이스를 인증하려면
1. 바탕 화면 아이콘을 클릭하여 StorSimple 스냅샷 관리자를 시작합니다.
2. **범위** 창에서 **장치** 를 클릭합니다.
3. **결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭한 다음 **인증** 을 클릭합니다.
4. **인증** 대화 상자가 나타납니다. 장치 암호를 입력한 다음 **확인** 을 클릭합니다.
   
    ![인증 대화 상자](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>디바이스 세부 정보 보기
다음 절차에 따라 StorSimple 디바이스의 세부 정보를 볼 수 있으며 필요한 경우 StorSimple 스냅샷 관리자와 디바이스를 다시 동기화할 수도 있습니다.

#### <a name="to-view-and-resynchronize-device-details"></a>디바이스 세부 정보를 보고 다시 동기화하려면
1. 바탕 화면 아이콘을 클릭하여 StorSimple 스냅샷 관리자를 시작합니다.
2. **범위** 창에서 **장치** 를 클릭합니다.
3. **결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭한 다음 **세부 정보** 를 클릭합니다.

4. **디바이스 세부 정보** 대화 상자가 표시됩니다. 이 상자에는 이름, 모델, 버전, 일련 번호, 상태, 대상 IQN(정규화된 iSCSI 이름), 마지막 동기화 날짜 및 시간이 표시됩니다.

* **다시 동기화** 를 클릭해 장치를 동기화합니다.
* **확인** 또는 **취소** 를 클릭해 대화 상자를 닫습니다.
  
  ![디바이스 세부 정보](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>개별 디바이스 새로 고침
다음 절차에 따라 개별 StorSimple 디바이스를 StorSimple 스냅샷 관리자와 다시 동기화할 수 있습니다.

#### <a name="to-refresh-a-device"></a>디바이스를 새로 고치려면
1. 바탕 화면 아이콘을 클릭하여 StorSimple 스냅샷 관리자를 시작합니다. 
2. **범위** 창에서 **장치** 를 클릭합니다. 
3. **결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭한 다음 **장치 새로 고침** 을 클릭합니다. 그러면 StorSimple 스냅샷 관리자와 디바이스가 동기화됩니다.

## <a name="delete-a-device-configuration"></a>디바이스 구성 삭제
다음 절차에 따라 개별 StorSimple 디바이스 구성을 StorSimple 스냅샷 관리자에서 삭제할 수 있습니다.

#### <a name="to-delete-a-device-configuration"></a>디바이스 구성을 삭제하려면
1. 바탕 화면 아이콘을 클릭하여 StorSimple 스냅샷 관리자를 시작합니다.
2. **범위** 창에서 **장치** 를 클릭합니다. 
3. **결과** 창에서 장치 이름을 마우스 오른쪽 단추로 클릭한 다음 **삭제** 를 클릭합니다. 
4. 다음과 같은 메시지가 나타납니다. **예** 를 클릭해 구성을 삭제하거나 **아니요** 를 클릭해 삭제를 취소합니다.
   
    ![디바이스 구성 삭제](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>만료된 디바이스 암호 변경
다음 절차에 따라 StorSimple 스냅샷 관리자에서 StorSimple 디바이스를 인증하기 위한 암호를 입력할 수 있습니다. Windows PowerShell 인터페이스를 사용하여 디바이스를 설정할 때 이 암호를 구성합니다. 그러나 암호는 만료될 수 있습니다. 이 경우에는 Azure 클래식 포털을 사용하여 암호를 변경할 수 있습니다. 그런 다음, 암호가 만료되기 전에 StorSimple 스냅샷 관리자에서 디바이스를 구성했기 때문에 StorSimple 스냅샷 관리자에서 디바이스를 다시 인증해야 합니다.

#### <a name="to-change-the-expired-password"></a>만료된 암호를 변경하려면
1. Azure 클래식 포털에서 StorSimple Manager 서비스를 시작합니다.
2. 장치   >  에 대해 장치 **구성** 을 클릭 합니다.
3. StorSimple 스냅샷 관리자 섹션으로 스크롤합니다. 14-15자로 암호를 입력합니다. 암호에는 대문자, 소문자, 숫자 및 특수 문자가 포함되어야 합니다.
4. 확인을 위해 암호를 다시 입력합니다.
5. 페이지 맨 아래에서 **저장** 을 클릭합니다.

#### <a name="to-re-authenticate-the-device"></a>디바이스를 다시 인증하려면
1. StorSimple 스냅샷 관리자를 시작합니다.
2. **범위** 창에서 **장치** 를 클릭합니다. 구성된 디바이스 목록이 **결과** 창에 표시됩니다.
3. 디바이스를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **인증** 을 클릭합니다.
4. **인증** 창에서 새 암호를 입력합니다.
5. 디바이스를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **디바이스 새로 고침** 을 선택합니다. 그러면 StorSimple 스냅샷 관리자와 디바이스가 동기화됩니다.

## <a name="replace-a-failed-device"></a>실패한 디바이스 바꾸기
StorSimple 디바이스에서 오류가 발생하여 대기(장애 조치(failover)) 디바이스로 교체하는 경우 다음 단계에 따라 새 디바이스에 연결하고 연결된 백업을 확인할 수 있습니다.

#### <a name="to-connect-to-a-new-device-after-failover"></a>장애 조치(failover) 후 새 디바이스에 연결하려면
1. 새 디바이스에 대한 iSCSI 연결을 다시 구성합니다. 자세한 지침은 [온-프레미스 StorSimple 디바이스 배포](storsimple-8000-deployment-walkthrough-u2.md)에서 "7단계: 볼륨 탑재, 초기화 및 포맷"을 참조하세요.

> [!NOTE]
> 새 StorSimple 디바이스에 이전 디바이스와 동일한 IP 주소가 있으면 이전 구성을 연결할 수 있습니다.


1. Microsoft StorSimple 관리 서비스를 중지합니다.
   
   1. 서버 관리자를 시작합니다.
   2. 서버 관리자 대시보드의 **도구** 메뉴에서 **서비스** 를 선택합니다.
   3. **서비스** 창에서 **Microsoft StorSimple 관리 서비스** 를 선택합니다.
   4. 오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 중지** 를 클릭합니다.
2. 이전 디바이스 관련 구성 정보를 제거합니다.
   
   1. 파일 탐색기에서 C:\ProgramData\Microsoft\StorSimple\BACatalog로 이동합니다.
   2. BACatalog 폴더의 파일을 삭제합니다.
3. Microsoft StorSimple 관리 서비스를 다시 시작합니다.
   
   1. 서버 관리자 대시보드의 **도구** 메뉴에서 **서비스** 를 선택합니다.
   2. **서비스** 창에서 **Microsoft StorSimple 관리 서비스** 를 선택합니다.
   3. 오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 다시 시작** 을 클릭합니다.
4. StorSimple 스냅샷 관리자를 시작합니다.
5. 새 StorSimple 디바이스를 구성하려면 [StorSimple Snapshot Manager 배포](storsimple-snapshot-manager-deployment.md)에서 2단계: StorSimple 디바이스 연결의 단계를 완료합니다.
6. **범위** 창에서 최상위 노드(예제의 StorSimple Snapshot Manager)를 마우스 오른쪽 단추로 클릭한 다음, **가져오기 표시 토글** 을 클릭합니다. 
7. 가져온 볼륨 그룹과 백업을 StorSimple 스냅샷 관리자에서 볼 수 있으면 메시지가 나타납니다. **확인** 을 클릭합니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 스냅샷 관리자를 사용하여 StorSimple 솔루션을 관리](storsimple-snapshot-manager-admin.md)하는 방법을 알아봅니다.
* [StorSimple 스냅샷 관리자를 사용하여 볼륨을 보고 관리](storsimple-snapshot-manager-manage-volumes.md)하는 방법을 알아봅니다.


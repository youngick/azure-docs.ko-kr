---
title: '자습서: Azure IoT Central을 사용하여 용수 사용량 모니터링 앱 만들기'
description: '자습서: Azure IoT Central 애플리케이션 템플릿을 사용하여 용수 사용량 모니터링 애플리케이션을 만드는 방법을 알아봅니다.'
author: miriambrus
ms.author: miriamb
ms.date: 12/11/2020
ms.topic: tutorial
ms.service: iot-central
services: iot-central
manager: abjork
ms.openlocfilehash: 476a0c2d75dcbee5c1ed4d758e0cbc9d4726ff95
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97587199"
---
# <a name="tutorial-create-a-water-consumption-monitoring-application-with-azure-iot-central"></a>자습서: Azure IoT Central을 사용하여 용수 사용량 모니터링 애플리케이션 만들기

이 자습서에서는 IoT Central 용수 사용량 모니터링 애플리케이션 템플릿을 사용하여 Azure IoT Central 용수 사용량 모니터링 애플리케이션을 만드는 방법을 보여 줍니다.

이 자습서에서는 다음 작업 방법을 배웁니다.

> [!div class="checklist"]
> * Azure IoT Central 용수 사용량 모니터링 템플릿을 사용하여 용수 사용량 모니터링 애플리케이션을 만듭니다.
> * 운영자 대시보드를 살펴보기 및 사용자 지정합니다.
> * 디바이스 템플릿을 살펴봅니다.
> * 시뮬레이션된 디바이스를 살펴봅니다.
> * 규칙을 살펴보고 구성합니다.
> * 작업을 구성합니다.
> * 흰색 레이블 지정을 사용하여 애플리케이션 브랜딩을 사용자 지정합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 다음이 필요합니다.

- Azure 구독 Azure 구독이 아직 없는 경우 [Azure 가입 페이지](https://aka.ms/createazuresubscription)에서 만들 수 있습니다.

## <a name="create-a-water-consumption-monitoring-app-with-azure-iot-central"></a>Azure IoT Central을 사용하여 용수 사용량 모니터링 앱 만들기

이 섹션에서는 Azure IoT Central 용수 사용량 모니터링 템플릿을 사용하여 Azure IoT Central에서 용수 사용량 모니터링 애플리케이션을 만듭니다.

새 Azure IoT Central 용수 사용량 모니터링 애플리케이션을 만들려면 다음을 수행합니다.

1. [Azure IoT Central 홈페이지](https://aka.ms/iotcentral) 웹 사이트로 이동합니다.

    Azure 구독이 있으면 액세스하는 데 사용하는 자격 증명을 사용하여 로그인합니다. 그렇지 않으면 Microsoft 계정을 사용하여 로그인합니다.

    ![조직 계정 입력](media/tutorial-waterconsumptionmonitoring/sign-in.png)

1. 왼쪽 창에서 **빌드** 를 선택하고 **정부** 탭을 선택합니다. **정부** 페이지에는 몇 가지 정부 애플리케이션 템플릿이 표시됩니다.

   ![정부 앱 빌드 템플릿](./media/tutorial-waterconsumptionmonitoring/iotcentral-government-tab-overview1.png)

1. **용수 사용량 모니터링** 애플리케이션 템플릿을 선택합니다.
이 템플릿에는 용수 사용량 디바이스 템플릿 샘플, 시뮬레이션된 디바이스, 운영자 대시보드 및 미리 구성된 모니터링 규칙이 포함되어 있습니다.

1. **앱 만들기** 를 선택하여 다음 필드가 있는 **새 애플리케이션** 만들기 양식을 엽니다.
    * **애플리케이션 이름**: 이 애플리케이션에서는 기본적으로 *용수 사용량 모니터링* 뒤에 Azure IoT Central에서 생성하는 고유한 ID 문자열을 사용합니다. 필요에 따라 친숙한 애플리케이션 이름을 선택해도 됩니다. 애플리케이션 이름은 나중에 변경할 수도 있습니다.
    * **URL**: Azure IoT Central에서 애플리케이션 이름에 기반한 URL을 자동으로 생성합니다. URL을 원하는 대로 업데이트하도록 선택할 수 있습니다. URL도 나중에 변경할 수 있습니다.
    * Azure 구독이 있는 경우 **디렉터리**, **Azure 구독** 및 **위치** 정보를 입력합니다. 구독이 없는 경우 **7일 평가판** 옵션을 선택하고 필요한 연락처 정보를 작성할 수 있습니다.

    디렉터리 및 구독에 대한 자세한 내용은 [애플리케이션 만들기 빠른 시작](../core/quick-deploy-iot-central.md)을 참조하세요.

1. 페이지의 맨 아래에서 **만들기** 를 선택합니다.

    ![Azure IoT Central 새 애플리케이션 페이지](./media/tutorial-waterconsumptionmonitoring/new-application-waterconsumptionmonitoring.png)

    ![Azure IoT Central 청구 정보 페이지](./media/tutorial-waterconsumptionmonitoring/new-application-waterconsumptionmonitoring-billinginfo.png)

이제 Azure IoT Central 용수 사용량 모니터링 템플릿을 사용하여 용수 사용량 모니터링 앱을 만들었습니다.

용수 사용량 모니터링 애플리케이션은 다음과 같이 미리 구성된 상태로 제공됩니다.

* 작업자 대시보드 샘플
* 미리 정의된 용수 흐름 및 밸브 디바이스 템플릿 샘플
* 시뮬레이션된 용수 흐름 및 스마트 밸브 디바이스
* 규칙 및 작업
* 흰색 레이블을 사용하여 샘플 브랜딩

빌드 중인 애플리케이션이므로 언제든지 수정할 수 있습니다. 이제 애플리케이션을 살펴보고 몇 가지 사용자 지정을 수행해 보겠습니다.

## <a name="explore-and-customize-the-operator-dashboard"></a>운영자 대시보드 살펴보기 및 사용자 지정

애플리케이션이 만들어지면 **Wide World 용수 사용량 대시보드** 샘플이 열립니다.

   ![용수 사용량 모니터링 대시보드](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-dashboardfull.png)

개발자는 운영자를 위한 대시보드 뷰를 만들고 사용자 지정할 수 있습니다. 먼저 대시보드를 살펴본 후에 사용자 지정을 수행해 보겠습니다.

> [!NOTE]
> 대시보드에 표시되는 모든 데이터는 시뮬레이션된 디바이스 데이터를 기반으로 하며 다음 섹션에서 살펴보겠습니다.
  
대시보드는 다음과 같은 여러 종류의 타일로 구성됩니다.

* **Wide World Water 수도 사업자 이미지 타일**: 대시보드의 첫 번째 타일은 가상의 수도 사업자인 "Wide World Water"에 대한 이미지 타일입니다. 이 타일은 사용자 고유의 이미지를 삽입하거나 제거하여 사용자 지정할 수 있습니다.
* **평균 용수 흐름 KPI 타일**: KPI 타일은 *지난 30분 동안의 평균* 예를 표시하도록 구성되어 있습니다. KPI 타일을 사용자 지정하고, 다른 유형과 시간 범위로 설정할 수 있습니다.
* **디바이스 명령 타일**: 이러한 타일로 **밸브 닫기**, **밸브 열기** 및 **밸브 위치 설정** 타일이 있습니다. 명령을 선택하면 시뮬레이션된 디바이스 명령 페이지로 이동합니다. Azure IoT Central에서 *명령* 은 *디바이스 기능* 유형입니다. 이 개념은 나중에 이 자습서의 "디바이스 템플릿" 섹션에서 살펴보겠습니다.
* **용수 분포 영역 맵**: 이 맵은 Azure IoT Central에서 직접 구성할 수 있는 Azure Maps를 사용합니다. 맵 타일에는 디바이스 위치가 표시됩니다. 마우스로 맵 위를 가리키면서 *확대*, *축소* 또는 *확장* 과 같은 컨트롤을 사용해 보세요.

    ![용수 사용량 모니터링 대시보드 맵](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-dashboard-map.png)

* **평균 용수 흐름 꺾은선형 차트** 및 **환경 상태 꺾은선형 차트**: 원하는 시간 범위에서 꺾은선형 차트로 그려지는 하나 이상의 디바이스 원격 분석을 시각화할 수 있습니다.
* **평균 밸브 압력 열 지도 차트**: 색 인덱스를 사용하여 시간 범위에 걸쳐 분산된 형태로 표시하려는 디바이스 원격 분석 데이터의 열 지도 시각화 형식을 선택할 수 있습니다.
* **경고 임계값 콘텐츠 다시 설정 타일**: 작업 호출 콘텐츠 타일 및 작업 페이지에 대한 링크를 포함할 수 있습니다. 이 경우 경고 임계값 다시 설정은 애플리케이션 **작업** 으로 이동하며, 여기서 디바이스 속성에 대한 업데이트를 실행할 수 있습니다. 이 옵션은 나중에 이 자습서의 "작업 구성" 섹션에서 살펴보겠습니다.
* **속성 타일**: 이 대시보드에는 **밸브 작동 정보**, **흐름 경고 임계값** 및 **유지 관리 정보** 타일이 표시됩니다.

### <a name="customize-the-dashboard"></a>대시보드 사용자 지정

작성자는 운영자의 대시보드에 대한 보기를 사용자 지정할 수 있습니다.

1. **편집** 을 선택하여 **Wide World 용수 사용량 대시보드** 를 사용자 지정합니다. **편집** 메뉴를 선택하여 대시보드를 사용자 지정할 수 있습니다. 대시보드가 **편집** 모드에 있으면 새 타일을 추가하거나 구성할 수 있습니다.

     ![대시보드 편집](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-edit-dashboard.png)

1. **+ 새로 만들기** 를 선택하여 새 대시보드를 만들고 처음부터 구성합니다. 대시보드가 여러 개 있을 수 있으며, 대시보드 메뉴에서 대시보드 간에 이동할 수 있습니다.

## <a name="explore-the-device-template"></a>디바이스 템플릿 살펴보기

Azure IoT Central의 디바이스 템플릿은 디바이스 기능을 정의하며, 디바이스 기능은 원격 분석, 속성 또는 명령일 수 있습니다. 작성자는 Azure IoT Central에서 연결할 디바이스의 기능을 나타내는 하나 이상의 디바이스 템플릿을 정의할 수 있습니다.

용수 사용량 모니터링 애플리케이션에는 *유량계* 및 *스마트 밸브* 디바이스를 나타내는 두 개의 참조 디바이스 템플릿이 제공됩니다.

디바이스 템플릿을 보려면 다음을 수행합니다.

1. Azure IoT Central에서 애플리케이션의 왼쪽 창에 있는 **디바이스 템플릿** 을 선택합니다. **디바이스 템플릿** 목록에서 **스마트 밸브** 및 **유량계** 라는 두 개의 디바이스 템플릿이 표시됩니다.

   ![디바이스 템플릿](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-devicetemplate.png)

1. **유량계** 디바이스 템플릿을 선택하고 디바이스 기능을 숙지합니다.

     ![유량계 디바이스 템플릿](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-devicetemplate-flowmeter.png)

### <a name="customize-the-device-template"></a>디바이스 템플릿 사용자 지정

디바이스 템플릿을 사용자 지정하려면 다음을 수행합니다.

1. **디바이스 템플릿** 메뉴에서 **사용자 지정** 으로 이동합니다.
1. `Temperature` 원격 분석 유형을 찾습니다.
1. `Temperature`의 **표시 이름** 을 `Reported temperature`로 업데이트합니다.
1. 측정 단위를 업데이트하거나 **최솟값** 및 **최댓값** 을 설정합니다.
1. **저장** 을 선택하여 변경 내용을 저장합니다.

### <a name="add-a-cloud-property"></a>클라우드 속성을 추가합니다.

1. **디바이스 템플릿** 메뉴에서 **클라우드 속성** 으로 이동합니다.
1. **+ 클라우드 속성 추가** 를 선택하여 새 클라우드 속성을 추가합니다.
    Azure IoT Central에서 디바이스와 관련된 속성을 추가할 수 있습니다. 예를 들어 클라우드 속성은 설치 영역, 자산 정보 또는 기타 유지 관리 정보와 관련된 경고 임계값일 수 있습니다.
1. **저장** 을 선택하여 변경 내용을 저장합니다.

### <a name="views"></a>보기

용수 사용량 모니터 디바이스 템플릿에는 미리 정의된 보기가 제공됩니다. 보기를 살펴보고 업데이트를 수행할 수 있습니다. 보기에서는 운영자가 디바이스 데이터를 표시하는 방법을 정의하지만, 클라우드 속성도 입력합니다.

  ![디바이스 템플릿 보기](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-devicetemplate-views.png)

### <a name="publish"></a>게시

변경 작업을 수행한 경우 디바이스 템플릿을 **게시** 해야 합니다.

### <a name="create-a-new-device-template"></a>새 디바이스 템플릿 만들기

**+ 새로 만들기** 를 선택하여 새 디바이스 템플릿을 만들고 만들기 프로세스를 수행합니다.
사용자 지정 디바이스 템플릿을 처음부터 만들거나 Azure 디바이스 카탈로그에서 디바이스 템플릿을 선택할 수 있습니다.

## <a name="explore-simulated-devices"></a>시뮬레이션된 디바이스 살펴보기

Azure IoT Central에서는 시뮬레이션된 디바이스를 만들어 디바이스 템플릿과 애플리케이션을 테스트할 수 있습니다. 용수 사용량 모니터링 애플리케이션에는 **유량계** 및 **스마트 밸브** 디바이스 템플릿에 매핑된 두 개의 시뮬레이션된 디바이스가 있습니다.

### <a name="view-the-devices"></a>디바이스 보기

1. 왼쪽 창에서 **디바이스 템플릿** > **모든 디바이스** 를 차례로 선택합니다.

   ![모든 디바이스 창](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-devices.png)

1. **스마트 밸브 1** 을 선택합니다.

    ![스마트 밸브 1](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitor-device1.png)

1. **명령** 탭에서 **스마트 밸브** 디바이스 템플릿에 정의된 기능인 세 가지 디바이스 명령(**밸브 열기**, **밸브 닫기** 및 **밸브 위치 설정**)을 볼 수 있습니다.

1. **디바이스 속성** 탭 및 **디바이스 대시보드** 탭을 살펴봅니다.

> [!NOTE]
> 모든 탭은 디바이스 템플릿 보기에서 구성됩니다.

### <a name="add-new-devices"></a>새 디바이스 추가

**디바이스** 탭에서 **+ 새로 만들기** 를 선택하여 새 디바이스를 추가합니다.

## <a name="explore-and-configure-rules"></a>규칙 살펴보기 및 구성

Azure IoT Central에서는 디바이스 원격 분석을 자동으로 모니터링하고 하나 이상의 조건이 충족되면 작업을 트리거하는 규칙을 만들 수 있습니다. 이메일 알림을 보내거나 Microsoft Power Automate 작업 또는 웹후크 작업을 트리거하여 데이터를 다른 서비스에 보내는 작업이 포함될 수 있습니다.

만든 용수 사용량 모니터링 애플리케이션에는 미리 구성된 세 가지 규칙이 있습니다.

### <a name="view-rules"></a>규칙 보기

1. 왼쪽 창에서 **규칙** 을 선택합니다.

   ![규칙 창](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-rules.png)

1. 애플리케이션의 미리 구성된 규칙 중 하나인 **높은 pH 경고** 를 선택합니다.

     ![높은 pH 경고](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-highflowalert.png)

    `High flow alert` 규칙은 `Acidity (pH)` 조건이 `Max flow threshold`보다 `greater than`인지 확인하도록 구성되었습니다. 최대 흐름 임계값은 **스마트 밸브** 디바이스 템플릿에 정의된 클라우드 속성입니다. `Max flow threshold` 값은 디바이스 인스턴스마다 설정됩니다.

이제 이메일 작업을 만들겠습니다.

규칙에 작업을 추가하려면 다음을 수행합니다.

1. **+메일** 을 선택합니다.
1. 작업의 친숙한 **표시 이름** 으로 **높은 pH 경고** 를 입력합니다.
1. **받는 사람** 에서 Azure IoT Central 계정과 연결된 이메일 주소를 입력합니다.
1. 필요에 따라 이메일 텍스트에 포함할 메모를 입력합니다.
1. **완료** 를 선택하여 작업을 완료합니다.
1. **저장** 을 선택하여 새 규칙을 저장하고 활성화합니다.

몇 분 내에 구성된 조건이 충족되면 이메일을 받게 됩니다.

> [!NOTE]
> 조건이 충족될 때마다 애플리케이션에서 이메일을 보냅니다. 자동화된 규칙에서 이메일 받기를 중지하는 규칙을 사용하지 않도록 설정하려면 **사용 안 함** 을 선택하세요.
  
새 규칙을 만들려면 다음을 수행합니다.

* 왼쪽 창의 **규칙** 탭에서 **+ 새로 만들기** 를 선택 합니다.

## <a name="configure-jobs"></a>작업 구성

Azure IoT Central에서 작업을 사용하면 여러 디바이스에서 디바이스 또는 클라우드 속성 업데이트를 트리거할 수 있습니다. 속성 외에도 작업을 사용하여 여러 디바이스에서 디바이스 명령을 트리거할 수 있습니다. Azure IoT Central에서는 워크플로를 자동화합니다.

1. 왼쪽 창에서 **작업** 을 선택합니다.
1. **+ 새로 만들기** 를 선택하고 하나 이상의 작업을 구성합니다.

## <a name="customize-your-application"></a>애플리케이션 사용자 지정

빌더는 여러 설정을 변경하여 애플리케이션에서 사용자 환경을 사용자 지정할 수 있습니다.

1. **관리** > **애플리케이션 사용자 지정** 을 차례로 선택합니다.
1. **애플리케이션 로고** 로 업로드할 이미지를 선택하려면 **변경** 단추를 선택합니다.
1. 브라우저 탭에 표시되는 **브라우저 아이콘** 이미지를 선택하려면 **변경** 단추를 선택합니다.
1. HTML 16진수 색 코드를 추가하여 기본 **브라우저 색** 을 바꿀 수도 있습니다.

   ![애플리케이션 로고, 브라우저 아이콘 및 브라우저 색 선택](./media/tutorial-waterconsumptionmonitoring/waterconsumptionmonitoring-customize-your-application.png)

1. **관리** > **애플리케이션 설정** 을 차례로 선택하여 애플리케이션 이미지를 변경할 수도 있습니다. 애플리케이션 이미지로 업로드할 이미지를 선택하려면 **이미지 선택** 단추를 선택합니다.
1. 마지막으로 애플리케이션의 오른쪽 위 모서리에서 **설정** 아이콘을 선택하여 **테마** 를 변경할 수도 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

이 애플리케이션을 계속 사용하지 않으려면 삭제합니다.

1. Azure IoT Central 애플리케이션의 왼쪽 창에서 **관리** 를 선택합니다.
1. **애플리케이션 설정** 을 선택한 다음, 페이지 아래쪽에서 **삭제** 를 선택합니다.

## <a name="next-steps"></a>다음 단계

* 자세한 정보 

> [!div class="nextstepaction"]
> [용수 사용량 모니터링 개념](./concepts-waterconsumptionmonitoring-architecture.md).

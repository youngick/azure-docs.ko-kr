---
title: 자습서 - Azure IoT Central 애플리케이션에서 규칙 만들기 및 관리
description: 이 자습서에서는 Azure IoT Central 규칙을 사용하여 디바이스를 거의 실시간으로 모니터링하고, 규칙이 트리거될 때 이메일 보내기와 같은 작업을 자동으로 호출하는 방법을 보여줍니다.
author: dominicbetts
ms.author: dobett
ms.date: 01/08/2021
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.openlocfilehash: b0b5aafd85fe6d992afa9d879f73ef0ec43e00d3
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99834377"
---
# <a name="tutorial-create-a-rule-and-set-up-notifications-in-your-azure-iot-central-application"></a>자습서: Azure IoT Central 애플리케이션에서 규칙 생성 및 알림 설정

*이 문서는 운영자, 빌더 및 관리자에게 적용됩니다.*

Azure IoT Central을 사용하여 원격으로 연결된 디바이스를 모니터링할 수 있습니다. Azure IoT Central 규칙을 사용하면 디바이스를 거의 실시간으로 모니터링하고 이메일 보내기 등의 작업을 자동으로 호출할 수 있습니다. 이 문서에서는 디바이스가 보내는 원격 분석을 모니터링하는 규칙을 만드는 방법을 설명합니다.

디바이스에서는 원격 분석을 사용하여 디바이스의 숫자 데이터를 보냅니다. 선택한 원격 분석이 지정된 임계값을 초과하면 규칙이 트리거됩니다.

이 자습서에서는 시뮬레이션된 센서 디바이스의 습도가 70&deg; F를 초과하는 경우 이메일을 보내는 규칙을 만듭니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
>
> * 규칙 만들기
> * 이메일 작업 추가

## <a name="prerequisites"></a>사전 요구 사항

시작하기 전에 [Azure IoT Central 애플리케이션 만들기](./quick-deploy-iot-central.md) 및 [IoT Central 애플리케이션에 시뮬레이션된 디바이스 추가](./quick-create-simulated-device.md) 빠른 시작을 완료하여 작업할 **센서 컨트롤러** 디바이스 템플릿을 만듭니다.

## <a name="create-a-rule"></a>규칙 만들기

원격 분석 규칙을 만들려면 디바이스 템플릿에 하나 이상의 원격 분석 값이 포함되어야 합니다. 이 자습서에서는 온도 및 습도 원격 분석 데이터를 전송하는 시뮬레이션된 **센서 컨트롤러** 디바이스를 사용합니다. [IoT Central 애플리케이션에 시뮬레이션된 디바이스 추가](./quick-create-simulated-device.md) 빠른 시작에서는 이 디바이스 템플릿을 추가하고 시뮬레이션된 디바이스를 만들었습니다. 이 규칙은 디바이스에서 보고한 온도를 모니터링하다가 온도가 70도를 초과하면 이메일을 보냅니다.

> [!NOTE]
> 애플리케이션당 규칙은 50개로 제한됩니다.

1. 왼쪽 창에서 **규칙** 을 선택합니다.

1. 아직 규칙을 하나도 만들지 않은 경우 다음 화면이 표시됩니다.

    :::image type="content" source="media/tutorial-create-telemetry-rules/rules-landing-page.png" alt-text="빈 규칙 목록을 보여주는 스크린샷":::

1. **+새로 만들기** 를 선택하여 새 규칙을 선택합니다.

1. 규칙 식별 이름으로 _온도 모니터링_ 을 입력하고 Enter 키를 누릅니다.

1. **센서 컨트롤러** 디바이스 템플릿을 선택합니다. 기본적으로 규칙은 디바이스 템플릿과 연결된 모든 디바이스에 자동으로 적용됩니다. 디바이스 하위 세트를 필터링하려면 **+ 필터** 를 선택하고, 디바이스 속성을 사용하여 디바이스를 식별합니다. 규칙을 사용하지 않도록 설정하려면 **사용/사용 안 함** 단추를 누릅니다.

    :::image type="content" source="media/tutorial-create-telemetry-rules/device-filters.png" alt-text="규칙 정의에서 디바이스 템플릿의 선택을 보여주는 스크린샷":::

### <a name="configure-the-rule-conditions"></a>규칙 조건 구성

조건은 규칙이 모니터링하는 조건을 정의합니다. 이 자습서에서는 온도가 70&deg; F를 초과하면 실행되는 규칙을 구성합니다.

1. **원격 분석** 드롭다운에서 **온도** 를 선택합니다.

1. 다음으로, **연산자** 로 **보다 큼** 을 선택하고 **값** 으로 _70_ 을 입력합니다.

    :::image type="content" source="media/tutorial-create-telemetry-rules/condition-filled-out.png" alt-text="규칙의 온도 조건을 보여주는 스크린샷":::

1. 선택 사항으로, **시간 집계** 를 설정할 수 있습니다. 시간 집계를 선택하는 경우 집계 드롭다운에서 평균 또는 합계와 같은 집계 유형도 선택해야 합니다.

    * 집계를 사용하지 않으면 조건을 충족하는 각 원격 분석 데이터 요소에 대해 규칙이 트리거됩니다. 예를 들어 온도가 70도를 초과할 때 트리거되도록 규칙을 구성하면 디바이스 온도가 이 값을 초과하면 거의 즉시 규칙이 트리거됩니다.
    * 집계를 사용하면 해당 시간 범위의 원격 분석 데이터 요소 집계 값이 조건을 충족할 때 규칙이 트리거됩니다. 예를 들어 온도가 70도를 초과하고 평균 시간 집계를 10분일 때 트리거하도록 규칙을 구성한 경우 디바이스가 10분 간격으로 계산하여 보고된 평균 온도가 70도를 초과하면 규칙이 트리거됩니다.

    :::image type="content" source="media/tutorial-create-telemetry-rules/aggregate-condition-filled-out.png" alt-text="작성된 집계 조건을 보여주는 스크린샷":::

**+ 조건** 을 선택하여 규칙에 여러 조건을 추가할 수 있습니다. 조건을 여러 개 지정하는 경우 모든 조건을 충족해야 규칙이 트리거됩니다. 각 조건은 암시적 `AND` 절을 통해 조인됩니다. 여러 조건이 있는 시간 집계를 사용하는 경우 모든 원격 분석 값을 집계해야 합니다.

### <a name="configure-actions"></a>작업 구성

조건을 정의한 후에는 규칙이 실행될 때 수행할 작업을 설정합니다. 규칙에 지정된 모든 조건이 true로 평가될 때 작업이 호출됩니다.

1. **작업** 섹션에서 **+ 이메일** 를 선택합니다.

1. 작업의 표시 이름으로 _온도 경고_ 를 입력하고, **받는 사람** 필드에 이메일 주소를 입력하고, 이메일 본문에 표시할 메모로 _디바이스를 확인해야 합니다!_ 를 입력합니다.

    > [!NOTE]
    > 애플리케이션에 추가되어 한 번 이상 로그인한 사용자에게만 이메일이 발송됩니다. Azure IoT Central에서 [사용자 관리](howto-administer.md)에 대해 자세히 알아보세요.

    :::image type="content" source="media/tutorial-create-telemetry-rules/configure-action.png" alt-text="규칙에 대한 이메일 작업을 보여주는 스크린샷":::

1. 작업을 저장하려면 **완료** 를 선택합니다. 규칙에 여러 작업을 추가할 수 있습니다.

1. 규칙을 저장하려면 **저장** 을 선택합니다. 몇 분 이내에 규칙이 적용되어 애플리케이션으로 전송되는 원격 분석 데이터의 모니터링이 시작됩니다. 규칙에 지정된 조건이 충족하는 경우 규칙이 구성된 이메일 작업을 트리거합니다.

잠시 후 규칙이 실행되면 이메일 메시지가 수신됩니다.

:::image type="content" source="media/tutorial-create-telemetry-rules/email.png" alt-text="알림 이메일을 보여주는 스크린샷":::

## <a name="delete-a-rule"></a>규칙 삭제

규칙이 더 이상 필요 없으면 해당 규칙을 열고 **삭제** 를 선택하여 삭제할 수 있습니다.

## <a name="enable-or-disable-a-rule"></a>규칙을 사용 또는 사용하지 않도록 설정

사용하도록 또는 사용하지 않도록 설정할 규칙을 선택합니다. 규칙의 **사용/사용 안 함** 단추를 눌러 규칙 범위에 포함되는 모든 디바이스에 규칙을 사용하도록 또는 사용하지 않도록 설정합니다.

## <a name="enable-or-disable-a-rule-for-specific-devices"></a>특정 디바이스에 규칙을 사용하도록 또는 사용하지 않도록 설정

사용자 지정할 규칙을 선택합니다. **대상 디바이스** 섹션에서 하나 이상의 필터를 사용하여 모니터링할 디바이스에 대한 규칙 범위를 좁힐 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [iot-central-clean-up-resources](../../../includes/iot-central-clean-up-resources.md)]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.

* 원격 분석 기반 규칙 만들기
* 작업 추가

임계값 기반 규칙을 정의했으므로, 그 다음으로 권장하는 단계는 다음과 같습니다.

> [!div class="nextstepaction"]
> [규칙에서 웹후크 만들기](./howto-create-webhooks.md)

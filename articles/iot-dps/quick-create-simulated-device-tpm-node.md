---
title: 빠른 시작 - Node.js를 사용하여 Azure IoT Hub에 시뮬레이트된 TPM 디바이스 프로비저닝
description: 빠른 시작 - Azure IoT Hub DPS(Device Provisioning Service)용 Node.js 디바이스 SDK를 사용하여 시뮬레이션된 TPM 디바이스를 만들고 프로비저닝합니다. 이 빠른 시작에서는 개별 등록을 사용합니다.
author: wesmc7777
ms.author: wesmc
ms.date: 11/08/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
ms.custom:
- mvc
- amqp
- mqtt
- devx-track-js
ms.openlocfilehash: 6e7e986f658570553763001afdd58d7bb1880f94
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94968182"
---
# <a name="quickstart-create-and-provision-a-simulated-tpm-device-using-nodejs-device-sdk-for-iot-hub-device-provisioning-service"></a>빠른 시작: IoT Hub Device Provisioning Service용 Node.js 디바이스 SDK를 사용하여 시뮬레이션된 TPM 디바이스 만들기 및 프로비전

[!INCLUDE [iot-dps-selector-quick-create-simulated-device-tpm](../../includes/iot-dps-selector-quick-create-simulated-device-tpm.md)]

이 빠른 시작에서는 Windows 컴퓨터에서 시뮬레이션 된 IoT 디바이스를 만듭니다. 시뮬레이션된 디바이스에는 HSM(하드웨어 보안 모듈)으로 TPM 시뮬레이터가 포함되어 있습니다. 디바이스 Node.js 코드 샘플을 사용하여 DPS(Device Provisioning Service)에서 개별 등록을 통해 이 시뮬레이션된 디바이스를 IoT 허브에 연결합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [프로비저닝](about-iot-dps.md#provisioning-process) 개념에 대해 잘 알아야 합니다.
- [Azure Portal에서 IoT Hub Device Provisioning Service 설정](./quick-setup-auto-provision.md) 완료
- 활성 구독이 있는 Azure 계정. [체험 계정 만들기](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
- [Node.js v4.0 이상](https://nodejs.org)
- [Git](https://git-scm.com/download/)

[!INCLUDE [IoT Device Provisioning Service basic](../../includes/iot-dps-basic.md)]

## <a name="prepare-the-environment"></a>환경 준비 

1. 컴퓨터에 [Node.js v4.0 이상](https://nodejs.org)이 설치되어 있는지 확인합니다.

1. 컴퓨터에 `git`이 설치되어 있고 명령 창에서 액세스할 수 있는 환경 변수에 추가되었는지 확인합니다. 설치할 `git` 도구의 최신 버전은 [Software Freedom Conservancy의 Git 클라이언트 도구](https://git-scm.com/download/)를 참조하세요. 여기에는 로컬 Git 리포지토리와 상호 작용하는 데 사용할 수 있는 명령줄 앱인 **Git Bash** 가 포함됩니다. 


## <a name="simulate-a-tpm-device"></a>TPM 디바이스 시뮬레이션

1. 명령 프롬프트 또는 Git Bash를 엽니다. `azure-utpm-c` GitHub 리포지토리를 복제합니다.
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-utpm-c.git --recursive
    ```

1. GitHub 루트 폴더로 이동하고, 시뮬레이션된 디바이스의 [HSM](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security/)이 되도록 [TPM](/windows/device-security/tpm/trusted-platform-module-overview) 시뮬레이터를 실행합니다. 포트 2321 및 2322에서 소켓을 수신 대기합니다. 이 명령 창을 닫지 마세요. 이 빠른 시작 가이드가 끝날 때까지 이 시뮬레이터를 계속 실행하고 있어야 합니다. 

    ```cmd/sh
    .\azure-utpm-c\tools\tpm_simulator\Simulator.exe
    ```

1. **registerdevice** 라는 빈 폴더를 새로 만듭니다. **registerdevice** 폴더의 명령 프롬프트에서 다음 명령을 사용하여 package.json 파일을 만듭니다. `npm`에서 요청하는 모든 질문에 답변하거나 사용자에게 적합한 경우 기본값을 적용합니다.
   
    ```cmd/sh
    npm init
    ```

1. 선도적인 다음 패키지를 설치합니다.

    ```cmd/sh
    npm install node-gyp -g
    npm install ffi -g
    ```

    > [!NOTE]
    > 위 패키지를 설치하는 데 알려진 몇 가지 문제가 있습니다. 이러한 문제를 해결하려면 **관리자 권한으로 실행** 모드에서 명령 프롬프트를 사용하여 `npm install --global --production windows-build-tools`를 실행하고, 경로를 설치된 버전으로 바꾼 후에 `SET VCTargetsPath=C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V140`을 실행한 다음, 위의 설치 명령을 다시 실행합니다.
    >

1. 등록 시 사용한 구성 요소가 포함된 다음 패키지를 설치합니다.

   - TPM에서 작동하는 보안 클라이언트: `azure-iot-security-tpm`
   - Device Provisioning Service에 연결하는 디바이스에 대한 전송: `azure-iot-provisioning-device-http` 또는 `azure-iot-provisioning-device-amqp`
   - 전송 및 보안 클라이언트를 사용하는 클라이언트: `azure-iot-provisioning-device`

     디바이스가 등록되면 등록 시 제공된 자격 증명을 사용하여 디바이스를 연결하기 위해 일반적인 IoT Hub Device Client 패키지를 사용할 수 있습니다. 필요한 항목은 다음과 같습니다.

   - 디바이스 클라이언트: `azure-iot-device`
   - 전송: `azure-iot-device-amqp`, `azure-iot-device-mqtt`, 또는 `azure-iot-device-http` 중 하나
   - 이미 설치한 보안 클라이언트: `azure-iot-security-tpm`

     > [!NOTE]
     > 아래 샘플에서는 `azure-iot-provisioning-device-http` 및 `azure-iot-device-mqtt` 전송을 사용합니다.
     > 

     **registerdevice** 폴더의 명령 프롬프트에서 다음 명령을 실행하여 이러한 패키지를 한 번에 모두 설치할 수 있습니다.

       ```cmd/sh
       npm install --save azure-iot-device azure-iot-device-mqtt azure-iot-security-tpm azure-iot-provisioning-device-http azure-iot-provisioning-device
       ```

1. 텍스트 편집기를 사용하여 **registerdevice** 폴더에 새 **ExtractDevice.js** 파일을 만듭니다.

1. **ExtractDevice.js** 파일의 시작 부분에 다음 `require` 문을 추가합니다.
   
    ```
    'use strict';

    var tpmSecurity = require('azure-iot-security-tpm');
    var tssJs = require("tss.js");

    var myTpm = new tpmSecurity.TpmSecurityClient(undefined, new tssJs.Tpm(true));
    ```

1. 메서드를 구현하는 다음 함수를 추가합니다.
   
    ```
    myTpm.getEndorsementKey(function(err, endorsementKey) {
      if (err) {
        console.log('The error returned from get key is: ' + err);
      } else {
        console.log('the endorsement key is: ' + endorsementKey.toString('base64'));
        myTpm.getRegistrationId((getRegistrationIdError, registrationId) => {
          if (getRegistrationIdError) {
            console.log('The error returned from get registration id is: ' + getRegistrationIdError);
          } else {
            console.log('The Registration Id is: ' + registrationId);
            process.exit();
          }
        });
      }
    });
    ```

1. **ExtractDevice.js** 파일을 저장하고 닫습니다. 샘플을 실행합니다.

    ```cmd/sh
    node ExtractDevice.js
    ```

1. 출력 창에 디바이스 등록에 필요한 **_인증 키_** 와 **_등록 ID_** 가 표시됩니다. 이러한 값을 기록해 둡니다. 


## <a name="create-a-device-entry"></a>디바이스 항목 만들기

Azure IoT Device Provisioning 서비스는 다음과 같은 두 가지 등록을 지원합니다.

- [등록 그룹](concepts-service.md#enrollment-group): 여러 관련 디바이스를 등록하는 데 사용됩니다.
- [개별 등록](concepts-service.md#individual-enrollment): 단일 디바이스를 등록하는 데 사용됩니다.

이 문서에서는 개별 등록을 보여 줍니다.

1. Azure Portal에 로그인하여 왼쪽 메뉴에서 **모든 리소스** 단추를 선택하고 Device Provisioning 서비스를 엽니다.

1. Device Provisioning Service 메뉴에서 **등록 관리** 를 선택합니다. **개별 등록** 탭을 선택하고 맨 위에서 **개별 등록 추가** 단추를 선택합니다. 

1. **등록 추가** 패널에서 다음 정보를 입력합니다.
   - ID 증명 *메커니즘* 으로 **TPM** 을 선택합니다.
   - 앞에서 기록한 값에서 TPM 디바이스에 대한 *등록 ID* 및 *인증 키* 를 입력합니다.
   - 프로비전 서비스와 연결된 IoT Hub를 선택합니다.
   - 필요에 따라 다음 정보를 입력합니다.
       - 고유한 *디바이스 ID* 를 입력합니다. 디바이스 이름을 지정할 때 중요한 데이터가 포함되지 않도록 합니다. 제공하지 않도록 선택하면 등록 ID가 대신 디바이스를 식별하는 데 사용됩니다.
       - 디바이스에 대해 원하는 초기 구성으로 **초기 디바이스 쌍 상태** 를 업데이트합니다.
   - 완료되면 **저장** 단추를 누릅니다. 

     ![포털 블레이드에 디바이스 등록 정보 입력](./media/quick-create-simulated-device/enter-device-enrollment.png)  

   성공적으로 등록되면 디바이스의 *등록 ID* 가 *개별 등록* 탭 아래의 목록에 표시됩니다. 


## <a name="register-the-device"></a>디바이스 등록

1. Azure Portal에서 Device Provisioning Service에 대한 **개요** 블레이드를 선택하고, **_글로벌 디바이스 엔드포인트_** 및 **_ID 범위_** 값을 적어 둡니다.

    ![포털 블레이드에서 디바이스 프로비저닝 서비스 엔드포인트 정보 추출](./media/quick-create-simulated-device/extract-dps-endpoints.png) 

1. 텍스트 편집기를 사용하여 **simDevice** 폴더에 새 **simDevice.js** 파일을 만듭니다.

1. **SimulatedDevice.js** 파일의 시작 부분에 다음 `require` 문을 추가합니다.
   
    ```
    'use strict';

    var ProvisioningTransport = require('azure-iot-provisioning-device-http').Http;
    var iotHubTransport = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var Message = require('azure-iot-device').Message;
    var tpmSecurity = require('azure-iot-security-tpm');
    var ProvisioningDeviceClient = require('azure-iot-provisioning-device').ProvisioningDeviceClient;
    ```

    > [!NOTE]
    > **Node.js용 Azure IoT SDK** 는 _AMQ_, _AMQP WS_ 및 _MQTT WS_ 와 같은 추가 프로토콜을 지원합니다.  더 많은 예제는 [Node.js 샘플용 Device Provisioning Service SDK](https://github.com/Azure/azure-iot-sdk-node/tree/master/provisioning/device/samples)를 참조하세요.
    > 

1. **globalDeviceEndpoint** 및 **idScope** 변수를 추가하고, 이러한 변수를 사용하여 **ProvisioningDeviceClient** 인스턴스를 만듭니다. **{globalDeviceEndpoint}** 및 **{idScope}** 를 **1단계** 의 **_전역 디바이스 엔드포인트_** 및 **_ID 범위_** 값으로 바꿉니다.
   
    ```
    var provisioningHost = '{globalDeviceEndpoint}';
    var idScope = '{idScope}';

    var tssJs = require("tss.js");
    var securityClient = new tpmSecurity.TpmSecurityClient('', new tssJs.Tpm(true));
    // if using non-simulated device, replace the above line with following:
    //var securityClient = new tpmSecurity.TpmSecurityClient();

    var provisioningClient = ProvisioningDeviceClient.create(provisioningHost, idScope, new ProvisioningTransport(), securityClient);
    ```

1. 디바이스에서 메서드를 실행하도록 다음 함수를 추가합니다.
   
    ```
    provisioningClient.register(function(err, result) {
      if (err) {
        console.log("error registering device: " + err);
      } else {
        console.log('registration succeeded');
        console.log('assigned hub=' + result.registrationState.assignedHub);
        console.log('deviceId=' + result.registrationState.deviceId);
        var tpmAuthenticationProvider = tpmSecurity.TpmAuthenticationProvider.fromTpmSecurityClient(result.registrationState.deviceId, result.registrationState.assignedHub, securityClient);
        var hubClient = Client.fromAuthenticationProvider(tpmAuthenticationProvider, iotHubTransport);

        var connectCallback = function (err) {
          if (err) {
            console.error('Could not connect: ' + err.message);
          } else {
            console.log('Client connected');
            var message = new Message('Hello world');
            hubClient.sendEvent(message, printResultFor('send'));
          }
        };

        hubClient.open(connectCallback);

        function printResultFor(op) {
          return function printResult(err, res) {
            if (err) console.log(op + ' error: ' + err.toString());
            if (res) console.log(op + ' status: ' + res.constructor.name);
            process.exit(1);
          };
        }
      }
    });
    ```

1. **RegisterDevice.js** 파일을 저장하고 닫습니다. 샘플을 실행합니다.

    ```cmd/sh
    node RegisterDevice.js
    ```

1. 디바이스를 부팅하고 IoT Hub 정보를 얻기 위해 Device Provisioning Service에 연결하는 과정을 시뮬레이션하는 메시지를 확인합니다. 프로비저닝 서비스와 연결된 IoT 허브에 시뮬레이션된 디바이스를 성공적으로 프로비저닝하면 디바이스 ID가 허브의 **IoT 디바이스** 블레이드에 표시됩니다. 

    ![디바이스가 IoT Hub에 등록됨](./media/quick-create-simulated-device/hub-registration.png) 

    디바이스에 대한 등록 항목의 기본값으로부터 *초기 디바이스 쌍 상태* 를 변경한 경우, 허브에서 원하는 쌍 상태를 가져와서 그에 맞게 작동할 수 있습니다. 자세한 내용은 [IoT Hub의 디바이스 쌍 이해 및 사용](../iot-hub/iot-hub-devguide-device-twins.md)을 참조하세요.


## <a name="clean-up-resources"></a>리소스 정리

디바이스 클라이언트 샘플을 계속해서 작업하고 탐색할 계획인 경우 이 빠른 시작에서 만든 리소스를 정리하지 마세요. 계속하지 않으려는 경우 다음 단계를 사용하여 이 빠른 시작에서 만든 모든 리소스를 삭제합니다.

1. 컴퓨터에서 디바이스 클라이언트 샘플 출력 창을 닫습니다.
1. 컴퓨터에서 TPM 시뮬레이터 창을 닫습니다.
1. Azure Portal의 왼쪽 메뉴에서 **모든 리소스** 를 선택한 다음, Device Provisioning Service를 선택합니다. 서비스에 대한 **등록 관리** 블레이드를 연 다음, **개별 등록** 탭을 선택합니다. 이 빠른 시작에 등록한 디바이스의 *등록 ID* 옆에 있는 확인란을 선택하고, 창 위쪽에 있는 **삭제** 단추를 누릅니다. 
1. Azure Portal의 왼쪽 메뉴에서 **모든 리소스** 를 선택한 다음, 사용자의 IoT 허브를 선택합니다. 허브에 대한 **IoT 디바이스** 블레이드를 열고, 이 빠른 시작에 등록한 디바이스의 *DEVICE ID* 옆에 있는 확인란을 선택한 다음, 창 위쪽에 있는 **삭제** 단추를 누릅니다.


## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 시뮬레이션된 TPM 디바이스를 머신에 만들고, IoT Hub Device Provisioning Service를 사용하여 IoT 허브에 이 디바이스를 프로비저닝했습니다. 프로그래밍 방식으로 TPM 디바이스를 등록하는 방법을 알아보려면 프로그래밍 방식으로 TPM 디바이스를 등록하는 빠른 시작을 계속 진행하세요. 

> [!div class="nextstepaction"]
> [Azure 빠른 시작 - Azure IoT Hub Device Provisioning Service에 TPM 디바이스 등록](quick-enroll-device-tpm-node.md)
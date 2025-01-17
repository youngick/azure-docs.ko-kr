---
title: 파일 포함
description: 포함 파일
services: azure-communication-services
author: mikben
manager: mikben
ms.service: azure-communication-services
ms.subservice: azure-communication-services
ms.date: 03/10/2021
ms.topic: include
ms.custom: include file
ms.author: mikben
ms.openlocfilehash: 9f62f262e1baa70982e667379a9bf4357197ecb4
ms.sourcegitcommit: 4bda786435578ec7d6d94c72ca8642ce47ac628a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103495473"
---
## <a name="prerequisites"></a>사전 요구 사항
시작하기 전에 다음을 확인해야 합니다.

- 활성 구독이 있는 Azure 계정을 만듭니다. 자세한 내용은 [체험 계정 만들기](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)를 참조하세요.
- [Node.js](https://nodejs.org/en/download/) 활성 LTS 및 유지 관리 LTS 버전(8.11.1 및 10.14.1 권장)을 설치합니다.
- Azure Communication Services 리소스를 만듭니다. 자세한 내용은 [Azure Communication 리소스 만들기](../../create-communication-resource.md)를 참조하세요. 이 빠른 시작에서는 **리소스 엔드포인트를 기록** 해야 합니다.
- ACS 사용자를 *세 명* 만들고 해당 사용자에게 [사용자 액세스 토큰](../../access-tokens.md)을 발급합니다. 범위를 **채팅** 으로 설정하고 **토큰 문자열과 userId 문자열을 기록** 해 둡니다. 전체 데모에서는 두 명의 초기 참가자가 있는 스레드를 만든 다음, 세 번째 참가자를 스레드에 추가합니다.

## <a name="setting-up"></a>설치

### <a name="create-a-new-web-application"></a>새 웹 애플리케이션 만들기

먼저 터미널 또는 명령 창을 열어 앱에 대한 새 디렉터리를 만들고 해당 디렉터리로 이동합니다.

```console
mkdir chat-quickstart && cd chat-quickstart
```

`npm init -y`를 실행하여 기본 설정으로 **package.json** 파일을 만듭니다.

```console
npm init -y
```

### <a name="install-the-packages"></a>패키지 설치

`npm install` 명령을 사용하여 아래 JavaScript용 Communication Services 클라이언트 라이브러리를 설치합니다.

```console
npm install @azure/communication-common --save

npm install @azure/communication-identity --save

npm install @azure/communication-signaling --save

npm install @azure/communication-chat --save

```

`--save` 옵션은 라이브러리를 **package.json** 파일의 종속성으로 나열합니다.

### <a name="set-up-the-app-framework"></a>앱 프레임워크 설정

이 빠른 시작에서는 webpack을 사용하여 애플리케이션 자산을 번들로 묶습니다. 다음 명령을 실행하여 webpack, webpack-cli 및 webpack-dev-server npm 패키지를 설치하고 **package.json** 에서 개발 종속성으로 나열합니다.

```console
npm install webpack webpack-cli webpack-dev-server --save-dev
```

프로젝트의 루트 디렉터리에 **index.html** 파일을 만듭니다. 이 파일을 템플릿으로 사용하여 JavaScript용 Azure Communication Chat 클라이언트 라이브러리를 사용하는 채팅 기능을 추가합니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Communication Client - Chat Sample</title>
  </head>
  <body>
    <h4>Azure Communication Services</h4>
    <h1>Chat Quickstart</h1>
    <script src="./bundle.js"></script>
  </body>
</html>
```

이 빠른 시작에 대한 애플리케이션 로직을 포함하기 위해 **client.js** 라는 프로젝트의 루트 디렉터리에 파일을 만듭니다.

### <a name="create-a-chat-client"></a>채팅 클라이언트 만들기

웹앱에서 채팅 클라이언트를 만들려면 Communications Service **엔드포인트** 와 필수 조건 단계의 일부로 생성된 **액세스 토큰** 을 사용합니다.

사용자 액세스 토큰을 사용하면 Azure Communication Services에 직접 인증되는 클라이언트 애플리케이션을 빌드할 수 있습니다. 이 빠른 시작에서는 채팅 애플리케이션에 대한 토큰을 관리하는 서비스 계층을 만드는 방법을 다루지 않습니다. 채팅 아키텍처에 대한 자세한 내용은 [채팅 개념](../../../concepts/chat/concepts.md)을, 액세스 토큰에 대한 자세한 내용은 [사용자 액세스 토큰](../../access-tokens.md)을 참조하세요.

**client.js** 내부에서 아래 코드의 엔드포인트 및 액세스 토큰을 사용하여 JavaScript용 Azure Communication Chat 클라이언트 라이브러리를 사용하는 채팅 기능을 추가합니다.

```JavaScript

import { ChatClient } from '@azure/communication-chat';
import { AzureCommunicationTokenCredential } from '@azure/communication-common';

// Your unique Azure Communication service endpoint
let endpointUrl = 'https://<RESOURCE_NAME>.communication.azure.com';
// The user access token generated as part of the pre-requisites
let userAccessToken = '<USER_ACCESS_TOKEN>';

let chatClient = new ChatClient(endpointUrl, new AzureCommunicationTokenCredential(userAccessToken));
console.log('Azure Communication Chat client created!');
```
- **endpointUrl** 을 Communication Services 리소스 엔드포인트로 바꿉니다. 아직 만들지 않았다면 [Azure 통신 리소스 만들기](../../create-communication-resource.md)를 참조하세요.
- **userAccessToken** 을 발급한 토큰으로 바꿉니다.


### <a name="run-the-code"></a>코드 실행

`webpack-dev-server`를 사용하여 앱을 빌드하고 실행합니다. 다음 명령을 실행하여 로컬 웹 서버에 애플리케이션 호스트를 번들로 묶습니다.
```console
npx webpack-dev-server --entry ./client.js --output bundle.js --debug --devtool inline-source-map
```
브라우저를 열고 http://localhost:8080/로 이동합니다.
브라우저 내 개발자 도구 콘솔에 다음이 표시됩니다.

```console
Azure Communication Chat client created!
```

## <a name="object-model"></a>개체 모델
다음 클래스 및 인터페이스는 JavaScript용 Azure Communication Services 채팅 클라이언트 라이브러리의 주요 기능 중 일부를 처리합니다.

| 이름                                   | 설명                                                                                                                                                                           |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ChatClient | 이 클래스는 채팅 기능에 필요합니다. 구독 정보를 사용하여 인스턴스화하고 스레드를 만들고 가져오고 삭제하는 데 사용합니다. |
| ChatThreadClient | 이 클래스는 채팅 스레드 기능에 필요합니다. ChatClient를 통해 인스턴스를 확보하여 메시지 보내기/받기/업데이트/삭제, 사용자 추가/제거/받기, 입력 알림 보내기, 읽음 확인, 채팅 이벤트 구독에 사용할 수 있습니다. |


## <a name="start-a-chat-thread"></a>채팅 스레드 시작

`createThread` 메서드를 사용하여 채팅 스레드를 만듭니다.

`createThreadRequest`는 스레드 요청을 설명하는 데 사용됩니다.

- 이 채팅에 토픽을 제공하려면 `topic`을 사용하세요. `UpdateThread` 함수를 사용하여 채팅 스레드를 만든 후에 토픽을 업데이트할 수 있습니다.
- `participants`를 사용하여 채팅 스레드에 추가할 참가자를 나열합니다.

확인되면 `createChatThread` 메서드가 `CreateChatThreadResult`를 반환합니다. 이 모델에는 새로 만든 스레드의 `id`에 액세스할 수 있는 `chatThread` 속성이 포함되어 있습니다. 그리고 `id`를 사용하여 `ChatThreadClient`의 인스턴스를 가져올 수 있습니다. 그런 다음, `ChatThreadClient`를 사용하여 메시지 보내기 또는 참가자 나열과 같은 작업을 스레드 내에서 수행할 수 있습니다.

```JavaScript
async function createChatThread() {
    let createThreadRequest = {
        topic: 'Preparation for London conference',
        participants: [{
                    id: { communicationUserId: '<USER_ID_FOR_JACK>' },
                    displayName: 'Jack'
                }, {
                    id: { communicationUserId: '<USER_ID_FOR_GEETA>' },
                    displayName: 'Geeta'
                }]
    };
    let createChatThreadResult = await chatClient.createChatThread(createThreadRequest);
    let threadId = createChatThreadResult.chatThread.id;
    return threadId;
    }

createChatThread().then(async threadId => {
    console.log(`Thread created:${threadId}`);
    // PLACEHOLDERS
    // <CREATE CHAT THREAD CLIENT>
    // <RECEIVE A CHAT MESSAGE FROM A CHAT THREAD>
    // <SEND MESSAGE TO A CHAT THREAD>
    // <LIST MESSAGES IN A CHAT THREAD>
    // <ADD NEW PARTICIPANT TO THREAD>
    // <LIST PARTICIPANTS IN A THREAD>
    // <REMOVE PARTICIPANT FROM THREAD>
    });
```

**USER_ID_FOR_JACK** 과 **USER_ID_FOR_GEETA** 를 사용자 및 토큰([사용자 액세스 토큰](../../access-tokens.md)) 생성 과정에서 얻은 사용자 ID로 바꿉니다.

브라우저 탭을 새로 고치면 콘솔에 다음이 표시됩니다.
```console
Thread created: <thread_id>
```

## <a name="get-a-chat-thread-client"></a>채팅 스레드 클라이언트 가져오기

`getChatThreadClient` 메서드는 이미 존재하는 스레드의 `chatThreadClient`를 반환합니다. 생성된 스레드에서 참가자 추가, 메시지 보내기 등의 작업을 수행하는 데 사용할 수 있습니다. threadId는 기존 채팅 스레드의 고유 ID입니다.

```JavaScript
let chatThreadClient = chatClient.getChatThreadClient(threadId);
console.log(`Chat Thread client for threadId:${threadId}`);

```
**client.js** 에서 `<CREATE CHAT THREAD CLIENT>` 주석 대신 이 코드를 추가하고, 브라우저 탭을 새로 고친 후 콘솔을 확인하면 다음이 보입니다.
```console
Chat Thread client for threadId: <threadId>
```

## <a name="send-a-message-to-a-chat-thread"></a>채팅 스레드에 메시지 보내기

`sendMessage` 메서드를 사용하여 threadId로 식별되는 스레드에 메시지를 보냅니다.

`sendMessageRequest`는 메시지 요청을 설명하는 데 사용됩니다.

- `content`를 사용하여 채팅 메시지 콘텐츠를 제공합니다.

`sendMessageOptions`는 작업 선택적 매개 변수를 설명하는 데 사용됩니다.

- `senderDisplayName`을 사용하여 보낸 사람의 표시 이름을 지정합니다.
- `type`을 사용하여 메시지 유형(예: 'text' 또는 'html')을 지정합니다.

`SendChatMessageResult`는 메시지 전송 후 반환된 응답이며, 메시지의 고유 ID인 ID를 포함합니다.

```JavaScript
let sendMessageRequest =
{
    content: 'Hello Geeta! Can you share the deck for the conference?'
};
let sendMessageOptions =
{
    senderDisplayName : 'Jack',
    type: 'text'
};
let sendChatMessageResult = await chatThreadClient.sendMessage(sendMessageRequest, sendMessageOptions);
let messageId = sendChatMessageResult.id;
```

**client.js** 에서 `<SEND MESSAGE TO A CHAT THREAD>` 주석 대신 이 코드를 추가하고, 브라우저 탭을 새로 고친 후 콘솔을 확인합니다.
```console
Message sent!, message id:<number>
```

## <a name="receive-chat-messages-from-a-chat-thread"></a>채팅 스레드에서 채팅 메시지 받기

실시간 신호를 통해, 새로 들어오는 메시지를 수신 대기하도록 구독하고 메모리의 현재 메시지를 적절하게 업데이트할 수 있습니다. Azure Communication Services는 [구독할 수 있는 이벤트 목록](../../../concepts/chat/concepts.md#real-time-signaling)을 지원합니다.

```JavaScript
// open notifications channel
await chatClient.startRealtimeNotifications();
// subscribe to new notification
chatClient.on("chatMessageReceived", (e) => {
    console.log("Notification chatMessageReceived!");
    // your code here
});

```
**client.js** 에서 `<RECEIVE A CHAT MESSAGE FROM A CHAT THREAD>` 주석 대신 이 코드를 추가합니다.
브라우저 탭을 새로 고치면 콘솔에 `Notification chatMessageReceived` 메시지가 표시됩니다.

또는 지정된 간격으로 `listMessages` 메서드를 폴링하여 채팅 메시지를 가져올 수 있습니다.

```JavaScript

let pagedAsyncIterableIterator = await chatThreadClient.listMessages();
let nextMessage = await pagedAsyncIterableIterator.next();
    while (!nextMessage.done) {
        let chatMessage = nextMessage.value;
        console.log(`Message :${chatMessage.content}`);
        // your code here
        nextMessage = await pagedAsyncIterableIterator.next();
    }

```
**client.js** 에서 `<LIST MESSAGES IN A CHAT THREAD>` 주석 대신 이 코드를 추가합니다.
탭을 새로 고치면 채팅 스레드에서 보낸 메시지 목록을 콘솔에서 찾을 수 있습니다.


`listMessages`는 `updateMessage` 및 `deleteMessage`를 사용하여 메시지에 발생한 편집 또는 삭제를 포함한 최신 버전의 메시지를 반환합니다.
삭제된 메시지의 경우 `chatMessage.deletedOn`은 메시지가 삭제된 시기를 나타내는 날짜/시간 값을 반환합니다. 편집된 메시지의 경우 `chatMessage.editedOn`은 메시지가 편집된 시간을 나타내는 datetime을 반환합니다. 원래 메시지 생성 시간은 메시지를 정렬하는 데 사용할 수 있는 `chatMessage.createdOn`을 사용하여 액세스할 수 있습니다.

`listMessages`는 `chatMessage.type`으로 식별할 수 있는 다양한 유형의 메시지를 반환합니다. 그 유형은 다음과 같습니다.

- `Text`: 스레드 참가자가 보낸 일반 채팅 메시지입니다.

- `ThreadActivity/TopicUpdate`: 주제가 업데이트되었음을 나타내는 시스템 메시지입니다.

- `ThreadActivity/AddParticipant`: 한 명 이상의 참가자가 채팅 스레드에 추가되었음을 나타내는 시스템 메시지입니다.

- `ThreadActivity/RemoveParticipant`: 참가자가 채팅 스레드에서 제거되었음을 나타내는 시스템 메시지입니다.

자세한 내용은 [메시지 유형](../../../concepts/chat/concepts.md#message-types)을 참조하세요.

## <a name="add-a-user-as-a-participant-to-the-chat-thread"></a>채팅 스레드에 사용자를 참가자로 추가

채팅 스레드가 생성되면 스레드에서 사용자를 추가하고 제거할 수 있습니다. 사용자를 추가하면 채팅 스레드에 메시지를 보내고 다른 참가자를 추가/제거할 수 있는 액세스 권한이 사용자에게 부여됩니다.

`addParticipants` 메서드를 호출하기 전에 해당 사용자에 대한 새 액세스 토큰 및 ID를 획득했는지 확인하세요. 사용자가 채팅 클라이언트를 초기화하려면 액세스 토큰이 필요합니다.

`addParticipantsRequest`는 `participants`가 채팅 스레드에 추가될 참가자를 나열하는 요청 개체를 설명합니다.
- `id`(필수)는 채팅 스레드에 추가될 통신 식별자입니다.
- 선택 사항인 `displayName`은 스레드 참가자의 표시 이름입니다.
- 선택 사항인 `shareHistoryTime`은 채팅 기록이 참가자와 공유된 시간입니다. 채팅 스레드가 시작된 이후의 기록을 공유하려면 이 속성을 스레드 생성 날짜와 동일한 날짜 또는 그 이전의 날짜로 설정합니다. 참가자가 추가되기 전의 기록을 공유하지 않으려면 현재 날짜로 설정합니다. 일부 기록을 공유하려면 원하는 날짜로 설정합니다.

```JavaScript

let addParticipantsRequest =
{
    participants: [
        {
            id: { communicationUserId: '<NEW_PARTICIPANT_USER_ID>' },
            displayName: 'Jane'
        }
    ]
};

await chatThreadClient.addParticipants(addParticipantsRequest);

```
**NEW_PARTICIPANT_USER_ID** 를 [새 사용자 ID](../../access-tokens.md)로 바꾸고 **client.js** 에서 `<ADD NEW PARTICIPANT TO THREAD>` 주석 대신 이 코드를 추가합니다.

## <a name="list-users-in-a-chat-thread"></a>채팅 스레드에 사용자 나열
```JavaScript
async function listParticipants() {
   let pagedAsyncIterableIterator = await chatThreadClient.listParticipants();
   let next = await pagedAsyncIterableIterator.next();
   while (!next.done) {
      let user = next.value;
      console.log(`User :${user.displayName}`);
      next = await pagedAsyncIterableIterator.next();
   }
}
await listParticipants();
```
**client.js** 에서 `<LIST PARTICIPANTS IN A THREAD>` 주석 대신 이 코드를 추가하고, 브라우저 탭을 새로 고친 후 콘솔을 확인하면 스레드의 사용자에 대한 정보가 보입니다.

## <a name="remove-user-from-a-chat-thread"></a>채팅 스레드에서 사용자 제거

참가자를 추가하는 방법과 유사하게 채팅 스레드에서 참가자를 제거할 수 있습니다. 제거하려면 추가한 참가자의 ID를 추적해야 합니다.

`removeParticipant` 메서드를 사용합니다. 여기서 `participant`는 스레드에서 제거할 통신 사용자입니다.

```JavaScript

await chatThreadClient.removeParticipant({ communicationUserId: <PARTICIPANT_ID> });
await listParticipants();
```
**PARTICIPANT_ID** 를 이전 단계에서 사용한 사용자 ID로 바꿉니다(<NEW_PARTICIPANT_USER_ID>).
**client.js** 에서 `<REMOVE PARTICIPANT FROM THREAD>` 주석 대신 이 코드를 추가합니다.

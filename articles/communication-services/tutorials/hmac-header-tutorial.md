---
title: C#을 사용하여 HTTP 요청에 서명하는 방법을 알아봅니다.
titleSuffix: An Azure Communication Services tutorial
description: C#을 통해 Azure Communication Services에 대한 HTTP 요청에 서명하는 방법을 알아봅니다.
author: alexandra142
manager: soricos
services: azure-communication-services
ms.author: apistrak
ms.date: 03/10/2021
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: e9b24e981e472371e477cd4dd895e976f709b2fb
ms.sourcegitcommit: 4bda786435578ec7d6d94c72ca8642ce47ac628a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103490513"
---
# <a name="sign-an-http-request"></a>HTTP 요청 서명

이 자습서에서는 HMAC 서명을 사용하여 HTTP 요청에 서명하는 방법을 알아봅니다.

[!INCLUDE [Public Preview Notice](../includes/public-preview-include.md)]


[!INCLUDE [Sign an HTTP request C#](./includes/hmac-header-csharp.md)]

## <a name="clean-up-resources"></a>리소스 정리

Communication Services 구독을 정리하고 제거하려면 리소스 또는 리소스 그룹을 삭제합니다. 리소스 그룹을 삭제하면 해당 리소스 그룹에 연결된 다른 모든 리소스가 함께 삭제됩니다. [Azure Communication Services 리소스 정리](../quickstarts/create-communication-resource.md#clean-up-resources) 및 [Azure Functions 리소스 정리](../../azure-functions/create-first-function-vs-code-csharp.md#clean-up-resources)에 대해 자세히 알아볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [앱에 음성 통화 추가](../quickstarts/voice-video-calling/getting-started-with-calling.md)

다음을 수행할 수도 있습니다.

- [앱에 채팅 추가](../quickstarts/chat/get-started.md)
- [사용자 액세스 토큰 만들기](../quickstarts/access-tokens.md)
- [클라이언트 및 서버 아키텍처에 대한 자세한 정보](../concepts/client-and-server-architecture.md)
- [인증에 대한 자세한 정보](../concepts/authentication.md)

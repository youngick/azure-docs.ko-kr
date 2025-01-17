---
title: 빠른 시작 - SMS 메시지 보내기
titleSuffix: An Azure Communication Services quickstart
description: Azure Communication Services를 사용하여 SMS 메시지를 보내는 방법에 대해 알아봅니다.
author: mikben
manager: jken
services: azure-communication-services
ms.author: mikben
ms.date: 03/10/2021
ms.topic: overview
ms.service: azure-communication-services
ms.custom: tracking-python, devx-track-js
zone_pivot_groups: acs-js-csharp-java-python
ms.openlocfilehash: ed246cfc3929e2893087a99b7876138859d4667a
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "103488331"
---
# <a name="quickstart-send-an-sms-message"></a>빠른 시작: SMS 메시지 보내기

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]


[!INCLUDE [Regional Availability Notice](../../includes/regional-availability-include.md)]

> [!IMPORTANT]
> SMS 메시지는 미국 전화 번호로 송수신할 수 있습니다. 다른 지역에 있는 전화 번호는 아직 Communication Services SMS에서 지원되지 않습니다.
> 자세한 내용은 **[전화 번호 형식](../../concepts/telephony-sms/plan-solution.md)** 을 참조하세요.

::: zone pivot="programming-language-csharp"
[!INCLUDE [Send SMS with .NET client library](./includes/send-sms-net.md)]
::: zone-end

::: zone pivot="programming-language-javascript"
[!INCLUDE [Send SMS with JavaScript client library](./includes/send-sms-js.md)]
::: zone-end

::: zone pivot="programming-language-python"
[!INCLUDE [Send SMS with Python client library](./includes/send-sms-python.md)]
::: zone-end

::: zone pivot="programming-language-java"
[!INCLUDE [Send SMS with Java client library](./includes/send-sms-java.md)]
::: zone-end

## <a name="troubleshooting"></a>문제 해결

SMS 전달과 관련된 문제를 해결하기 위해 [Event Grid를 통해 전달 보고를 사용](./handle-sms-events.md)하여 전달 세부 정보를 캡처할 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

Communication Services 구독을 정리하고 제거하려면 리소스 또는 리소스 그룹을 삭제하면 됩니다. 리소스 그룹을 삭제하면 해당 리소스 그룹에 연결된 다른 모든 리소스가 함께 삭제됩니다. [리소스 정리](../create-communication-resource.md#clean-up-resources)에 대해 자세히 알아보세요.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 Azure Communication Services를 사용하여 SMS 메시지를 보내는 방법을 배웠습니다.

> [!div class="nextstepaction"]
> [SMS 이벤트 구독](./handle-sms-events.md)

> [!div class="nextstepaction"]
> [전화 번호 유형](../../concepts/telephony-sms/plan-solution.md)

> [!div class="nextstepaction"]
> [SMS에 대한 자세한 정보](../../concepts/telephony-sms/concepts.md)

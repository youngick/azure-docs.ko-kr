---
title: Azure Portal을 사용하여 Service Bus 토픽 및 구독 만들기
description: '빠른 시작: 이 빠른 시작에서는 Azure Portal을 사용하여 Service Bus 토픽 및 구독을 만드는 방법에 대해 알아봅니다.'
author: spelluru
ms.topic: quickstart
ms.date: 06/23/2020
ms.author: spelluru
ms.openlocfilehash: 749ba3d2947dfd7defdf2549305f2a61c16ba713
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "95803280"
---
# <a name="use-the-azure-portal-to-create-a-service-bus-topic-and-subscriptions-to-the-topic"></a>Azure Portal을 사용하여 Service Bus 토픽 및 해당 토픽에 대한 하나 이상의 구독 만들기
이 빠른 시작에서는 Azure Portal를 사용하여 Service Bus 토픽을 만든 다음, 해당 토픽에 대한 구독을 만듭니다. 

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Service Bus 토픽 및 구독 정의
Service Bus 토픽 및 구독은 *게시/구독* 메시징 통신 모델을 지원합니다. 토픽 및 구독을 사용하는 경우 분산 애플리케이션의 구성 요소가 서로 직접 통신하지 않고 중간자 역할을 하는 토픽을 통해 메시지를 교환합니다.

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

각 메시지가 단일 소비자에 의해 처리되는 Service Bus 큐와 반대로, 토픽과 구독은 게시/구독 패턴을 사용하여 일대다 형태의 통신을 제공합니다. 하나의 토픽에 여러 구독을 등록할 수 있습니다. 토픽에 메시지를 전송하면 각 구독에서 독립적으로 처리할 수 있습니다. 토픽 구독은 토픽에 전송된 메시지의 복사본을 받는 가상 큐와 유사합니다. 선택적으로 구독별 토픽에 대한 필터 규칙을 등록할 수 있으며, 이렇게 하면 각 토픽 구독에서 받는 토픽 메시지를 필터링하거나 제한할 수 있습니다.

Service Bus 토픽 및 구독을 사용하면 다수의 사용자와 애플리케이션에 대해 다수의 메시지를 처리하도록 확장할 수 있습니다.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-create-topics-three-subscriptions-portal](../../includes/service-bus-create-topics-three-subscriptions-portal.md)]

> [!NOTE]
> [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer/)로 Service Bus 리소스를 관리할 수 있습니다. Service Bus Explorer를 사용하면 Service Bus 네임스페이스에 연결하고 쉬운 방식으로 메시징 엔터티를 관리할 수 있습니다. 이 도구는 가져오기/내보내기 기능 또는 항목, 큐, 구독, 릴레이 서비스, Notification Hubs 및 이벤트 허브를 테스트하는 기능과 같은 고급 기능을 제공합니다. 

## <a name="next-steps"></a>다음 단계
이 문서에서는 Service Bus 네임스페이스, 네임스페이스의 항목 및 세 개의 구독을 만들었습니다. 항목에 메시지를 게시하고 구독에서 메시지를 구독하는 방법을 알아보려면 **메시지 게시 및 구독** 섹션에서 다음 빠른 시작 중 하나를 참조하세요. 

- [.NET](service-bus-dotnet-how-to-use-topics-subscriptions.md)
- [Java](service-bus-java-how-to-use-topics-subscriptions.md)
- [JavaScript](service-bus-nodejs-how-to-use-topics-subscriptions.md)
- [Python](service-bus-python-how-to-use-topics-subscriptions.md)
- [PHP](service-bus-php-how-to-use-topics-subscriptions.md)
- [Ruby](service-bus-ruby-how-to-use-topics-subscriptions.md)
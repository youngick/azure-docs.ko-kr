---
title: Queue Storage에 대한 성능 및 확장성 검사 목록 - Azure Storage
description: 고성능 애플리케이션을 개발할 때 Queue Storage에서 사용하는 방법에 대해 검증된 사례의 검사 목록입니다.
author: tamram
services: storage
ms.author: tamram
ms.date: 10/10/2019
ms.topic: overview
ms.service: storage
ms.subservice: queues
ms.custom: devx-track-csharp
ms.openlocfilehash: 4040a81d5b509ddbdd355953e28721a7c9fccfb8
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97585669"
---
<!-- docutune:casing "Timeout and Server Busy errors" -->

# <a name="performance-and-scalability-checklist-for-queue-storage"></a>Queue Storage에 대한 성능 및 확장성 검사 목록

Microsoft는 Queue Storage를 사용하여 고성능 애플리케이션을 개발하는 방법에 대해 검증된 다양한 사례를 개발했습니다. 이 검사 목록에서는 개발자가 성능을 최적화하기 위해 수행할 수 있는 주요 사례를 식별합니다. 애플리케이션을 설계하는 동안 프로세스 전체에서 이러한 사례를 명심하세요.

Azure Storage에는 용량, 트랜잭션 속도 및 대역폭에 대한 확장성 및 성능 목표가 있습니다. Azure Storage 확장성 목표에 대한 자세한 내용은 [표준 스토리지 계정의 확장성 및 성능 목표](../common/scalability-targets-standard-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) 및 [Queue Storage의 확장성 및 성능 목표](scalability-targets.md)를 참조하세요.

## <a name="checklist"></a>검사 목록

이 문서에서는 성능에 대해 검증된 사례를 Queue Storage 애플리케이션 개발 중에 수행할 수 있는 검사 목록으로 구성합니다.

| 완료된 | Category | 디자인 고려 사항 |
|--|--|--|
| &nbsp; | 확장성 목표 | [애플리케이션에서 최대 스토리지 계정 수를 초과하여 사용하지 않도록 디자인할 수 있습니까?](#maximum-number-of-storage-accounts) |
| &nbsp; | 확장성 목표 | [용량 및 트랜잭션 제한에 도달하지 않도록 방지하고 있습니까?](#capacity-and-transaction-targets) |
| &nbsp; | 네트워킹 | [클라이언트 쪽 디바이스에 필요한 성능을 달성할 수 있을 만큼 충분한 높은 대역폭과 짧은 대기 시간이 있습니까?](#throughput) |
| &nbsp; | 네트워킹 | [클라이언트 쪽 디바이스에 고품질 네트워크 링크가 있습니까?](#link-quality) |
| &nbsp; | 네트워킹 | [클라이언트 애플리케이션이 스토리지 계정과 동일한 지역에 있습니까?](#location) |
| &nbsp; | 직접 클라이언트 액세스 | [SAS(공유 액세스 서명)와 CORS(원본 간 리소스 공유)를 사용하여 Azure Storage에 직접 액세스할 수 있습니까?](#sas-and-cors) |
| &nbsp; | .NET 구성 | [최적의 성능을 달성하기 위해 .NET Core 2.1 이상을 사용하고 있습니까?](#use-net-core) |
| &nbsp; | .NET 구성 | [클라이언트가 충분한 수의 동시 연결을 사용하도록 구성했습니까?](#increase-default-connection-limit) |
| &nbsp; | .NET 구성 | [.NET 애플리케이션의 경우 .NET에서 충분한 수의 스레드를 사용하도록 구성했습니까?](#increase-the-minimum-number-of-threads) |
| &nbsp; | 병렬 처리 | [고객의 기능이 오버로드되지 않거나 확장성 목표에 도달하지 않도록 병렬 처리가 적절히 제한되도록 했습니까?](#unbounded-parallelism) |
| &nbsp; | 도구 | [Microsoft에서 제공하는 클라이언트 라이브러리와 도구의 최신 버전을 사용하고 있습니까?](#client-libraries-and-tools) |
| &nbsp; | 다시 시도 | [제한 오류 및 시간 제한에 대한 지수 백오프가 포함된 재시도 정책을 사용하고 있습니까?](#timeout-and-server-busy-errors) |
| &nbsp; | 다시 시도 | [애플리케이션에서 다시 시도할 수 없는 오류 발생 시에는 작업을 다시 시도하지 않습니까?](#non-retryable-errors) |
| &nbsp; | 구성 | [작은 요청의 성능을 향상시키기 위해 Nagle의 알고리즘을 해제했습니까?](#disable-nagles-algorithm) |
| &nbsp; | 메시지 크기 | [큐 성능을 개선하기 위해 메시지를 압축합니까?](#message-size) |
| &nbsp; | 대량 검색 | [여러 메시지를 단일 get 작업으로 검색하나요?](#batch-retrieval) |
| &nbsp; | 폴링 빈도 | [애플리케이션의 체감 대기 시간을 단축할 수 있을 만큼 자주 폴링을 수행하고 있습니까?](#queue-polling-interval) |
| &nbsp; | 메시지 업데이트 | [오류 발생 시 전체 메시지를 다시 처리할 필요가 없도록 메시지 처리 진행률을 저장하기 위해 업데이트 메시지 작업을 수행하고 있나요?](#perform-an-update-message-operation) |
| &nbsp; | Architecture | [장기 실행 작업을 중요 경로 외부에서만 실행하고 독립적으로 확장함으로써 큐를 통해 전체 애플리케이션의 확장성을 높이고 있습니까?](#application-architecture) |

## <a name="scalability-targets"></a>확장성 목표

애플리케이션이 확장성 목표에 도달하거나 목표를 초과하는 경우 트랜잭션 대기 시간이 길어지거나 제한이 증가할 수 있습니다. Azure Storage에서 애플리케이션을 제한하면 서비스에서 503(`Server Busy`) 또는 500(`Operation Timeout`) 오류 코드를 반환하기 시작합니다. 확장성 목표의 한도 내에서 유지하여 이러한 오류를 방지하는 것은 애플리케이션의 성능을 향상시키는 데 중요한 부분입니다.

Queue Storage의 확장성 목표에 대한 자세한 내용은 [Azure Storage 확장성 및 성능 목표](./scalability-targets.md#scale-targets-for-queue-storage)를 참조하세요.

### <a name="maximum-number-of-storage-accounts"></a>최대 스토리지 계정 수

특정 구독/지역 조합에 허용되는 최대 스토리지 계정 수에 도달하는 경우 여러 스토리지 계정을 사용하여 수신, 송신, IOPS(초당 I/O 작업 수) 또는 용량을 늘리도록 분할하고 있습니까? 이 시나리오에서는 가능한 경우 워크로드에 필요한 스토리지 계정 수를 줄이기 위해 스토리지 계정에 대한 제한을 늘리는 것이 좋습니다. 스토리지 계정에 대한 제한을 늘리도록 요청하려면 [Azure 지원](https://azure.microsoft.com/support/options/)에 문의하세요. 자세한 내용은 [더 크고 더 높은 규모의 스토리지 계정 발표](https://azure.microsoft.com/blog/announcing-larger-higher-scale-storage-accounts/)를 참조하세요.

### <a name="capacity-and-transaction-targets"></a>용량 및 트랜잭션 목표

애플리케이션이 특정 스토리지 계정의 확장성 목표에 도달한 경우 다음 방법 중 하나를 사용할 수 있습니다.

- 큐의 확장성 목표가 애플리케이션에 충분하지 않으면 여러 큐를 사용하여 메시지를 배포합니다.
- 애플리케이션이 확장성 목표에 도달하거나 목표를 초과한 원인이 되는 워크로드를 다시 고려합니다. 즉, 대역폭이나 용량을 더 적게 사용하거나 트랜잭션을 더 적게 수행하도록 해당 작업을 다시 디자인할 수 있는지를 파악합니다.
- 애플리케이션에서 확장성 목표 중 하나를 초과해야 하는 경우 여러 스토리지 계정을 만들어 애플리케이션 데이터를 해당 스토리지 계정에 분할합니다. 이러한 패턴을 사용하는 경우에는 향후 부하 분산을 위해 스토리지 계정을 더 추가할 수 있도록 애플리케이션을 디자인해야 합니다. 스토리지 계정 자체에는 저장된 데이터, 수행된 트랜잭션 또는 전송된 데이터와 관련된 사용량 이외의 비용은 없습니다.
- 애플리케이션의 대역폭 목표에 도달하는 경우 클라이언트 쪽의 데이터를 압축하여 Azure Storage에 보내는 데 필요한 대역폭을 줄이는 것이 좋습니다. 데이터를 압축하면 대역폭이 절약되고 네트워크 성능이 향상될 수 있지만 성능에 부정적인 영향을 미칠 수도 있습니다. 클라이언트 쪽의 데이터 압축 및 압축 풀기에 대한 추가 처리 요구 사항으로 인해 성능에 미치는 영향을 평가합니다. 압축된 데이터를 저장하면 표준 도구를 사용하여 데이터를 보는 것이 더 어려울 수 있으므로 문제 해결이 더 어려워 질 수 있습니다.
- 애플리케이션에서 확장성 목표에 도달하는 경우 재시도에 대해 지수 백오프를 사용하고 있는지 확인합니다. 이 문서에서 설명하는 추천 사항을 구현하여 확장성 목표에 도달하지 않도록 하는 것이 가장 좋습니다. 그러나 지수 백오프를 재시도에 사용하면 애플리케이션에서 빠르게 다시 시도하지 못하므로 제한 성능이 저하될 수 있습니다. 자세한 내용은 [시간 제한 및 서버 사용 중 오류](#timeout-and-server-busy-errors) 섹션을 참조하세요.

## <a name="networking"></a>네트워킹

애플리케이션의 실제 네트워크 제약 조건은 성능에 큰 영향을 미칠 수 있습니다. 다음 섹션에서는 사용자에게 발생할 수 있는 몇 가지 제한 사항에 대해 설명합니다.

### <a name="client-network-capability"></a>클라이언트 네트워크 기능

다음 섹션에서 설명한 대로 네트워크 링크의 대역폭과 품질은 애플리케이션 성능에서 중요한 역할을 합니다.

#### <a name="throughput"></a>처리량

대역폭의 경우에는 클라이언트 기능에 문제가 있는 경우가 많습니다. 대규모 Azure 인스턴스에는 용량이 더 많은 NIC가 포함되므로 머신 하나의 네트워크 한도를 높여야 하는 경우에는 더 큰 인스턴스나 더 많은 VM을 사용하는 것이 좋습니다. 온-프레미스 애플리케이션에서 Azure Storage에 액세스하는 경우에도 동일한 규칙이 적용됩니다. 즉, 클라이언트 디바이스의 네트워크 기능과 Azure Storage 위치에 대한 네트워크 연결을 파악하고, 필요한 경우 이를 향상시키거나 해당 기능 내에서 작동하도록 애플리케이션을 디자인해야 합니다.

#### <a name="link-quality"></a>링크 품질

네트워크 사용량과 마찬가지로 네트워크 조건으로 인해 오류와 패킷 손실이 발생하면 효과적인 처리량의 속도가 느려집니다. Wireshark 또는 네트워크 모니터를 사용하면 이 문제를 진단하는 데 도움이 될 수 있습니다.

### <a name="location"></a>위치

모든 분산 환경에서는 클라이언트를 서버 근처에 배치하면 성능을 최대화할 수 있습니다. Azure Storage 액세스 시 대기 시간을 최소화하려는 경우에는 클라이언트를 같은 Azure 지역 내에 배치하는 것이 가장 좋습니다. 예를 들어 Azure Storage를 사용하는 Azure 웹앱이 있는 경우 미국 서부 또는 동남 아시아와 같은 단일 지역 내에서 둘 다를 찾습니다. 리소스를 공동 배치하면 단일 지역 내의 대역폭 사용량이 무료이므로 대기 시간과 비용이 줄어듭니다.

모바일 디바이스 앱 또는 온-프레미스 엔터프라이즈 서비스와 같이 클라이언트 애플리케이션이 Azure Storage에 액세스하지만 Azure 내에서 호스팅되지 않는 경우 스토리지 계정을 해당 클라이언트와 가까운 지역에 배치하면 대기 시간을 줄일 수 있습니다. 고객이 광범위하게 분산되어 있는 경우(예: 북아메리카 및 유럽 일부) 지역당 하나의 스토리지 계정을 사용하는 것이 좋습니다. 애플리케이션에서 개별 사용자 관련 데이터를 저장하며 스토리지 계정 간에 데이터를 복제하지 않아도 되는 경우 이 방식을 보다 쉽게 구현할 수 있습니다.

## <a name="sas-and-cors"></a>SAS 및 CORS

Azure Storage의 데이터에 액세스할 수 있는 권한을 코드(예: 사용자의 웹 브라우저 또는 휴대폰 앱에서 실행되는 JavaScript)에 부여해야 한다고 가정합니다. 한 가지 방법은 프록시로 작동하는 서비스 애플리케이션을 구축하는 것입니다. 사용자의 디바이스는 서비스를 인증하여 Azure Storage 리소스에 대한 액세스 권한을 부여합니다. 이러한 방식을 사용하면 안전하지 않은 디바이스에서 스토리지 계정 키가 노출되는 상황을 방지할 수 있습니다. 그러나 이 방법은 사용자의 디바이스와 Azure Storage 간에 전송되는 모든 데이터가 서비스 애플리케이션을 통과해야 하므로 서비스 애플리케이션에 상당한 오버헤드가 발생합니다.

SAS(공유 액세스 서명)를 사용하여 서비스 애플리케이션을 Azure Storage의 프록시로 사용하지 않도록 방지할 수 있습니다. SAS를 사용하면 제한된 액세스 토큰을 사용하여 사용자의 디바이스에서 Azure Storage에 직접 요청할 수 있습니다. 예를 들어 사용자가 사진을 애플리케이션에 업로드하려는 경우 서비스 애플리케이션에서 SAS를 생성하여 사용자의 디바이스로 보낼 수 있습니다. SAS 토큰은 지정된 시간 간격 동안 Azure Storage 리소스에 쓸 수 있는 권한을 부여할 수 있으며, 그 후에는 SAS 토큰이 만료됩니다. SAS에 대한 자세한 내용은 [SAS(공유 액세스 서명)를 사용하여 Azure Storage 리소스에 대한 제한된 액세스 권한 부여](../common/storage-sas-overview.md)를 참조하세요.

일반적으로 웹 브라우저는 한 도메인의 웹 사이트에서 호스팅하는 페이지의 JavaScript에서 다른 도메인에 대한 쓰기 작업과 같은 특정 작업을 수행할 수 없습니다. 동일한 원본 정책이라고 하는 이 정책은 한 페이지의 악성 스크립트에서 다른 웹 페이지의 데이터에 액세스하지 못하도록 방지합니다. 그러나 클라우드에서 솔루션을 구축하는 경우 동일한 원본 정책이 제한될 수 있습니다. CORS(원본 간 리소스 공유)는 대상 도메인이 원본 도메인에서 시작된 요청을 신뢰하는 브라우저와 통신할 수 있게 하는 브라우저 기능입니다.

예를 들어 Azure에서 실행되는 웹 애플리케이션에서 Azure Storage 계정에 리소스를 요청한다고 가정합니다. 웹 애플리케이션은 원본 도메인이고, 스토리지 계정은 대상 도메인입니다. Azure Storage에서 원본 도메인의 요청을 신뢰하는 웹 브라우저와 통신하도록 모든 Azure Storage 서비스에 대해 CORS를 구성할 수 있습니다. CORS에 대한 자세한 내용은 [Azure Storage에 대한 CORS(원본 간 리소스 공유) 지원](/rest/api/storageservices/Cross-Origin-Resource-Sharing--CORS--Support-for-the-Azure-Storage-Services)을 참조하세요.

SAS 및 CORS는 모두 웹 애플리케이션에서 불필요한 로드를 방지하는 데 도움이 될 수 있습니다.

## <a name="net-configuration"></a>.NET 구성

이 섹션에서는 .NET Framework를 사용하는 경우 성능을 크게 개선하기 위해 사용할 수 있는 다양한 빠른 구성 설정을 소개합니다. 다른 언어를 사용하는 경우에는 선택한 언어에 비슷한 개념이 적용되는지 확인하세요.

### <a name="use-net-core"></a>.NET Core 사용

성능 향상을 활용하려면 .NET Core 2.1 이상을 사용하여 Azure Storage 애플리케이션을 개발합니다. 가능하면 .NET Core 3.x를 사용하는 것이 좋습니다.

.NET Core의 성능 향상에 대한 자세한 내용은 다음 블로그 게시물을 참조하세요.

- [.NET Core 3.0의 성능 향상](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-core-3-0/)
- [.NET Core 2.1의 성능 향상](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-core-2-1/)

### <a name="increase-default-connection-limit"></a>기본 연결 제한 늘리기

.NET에서 다음 코드는 기본 연결 제한(일반적으로 클라이언트 환경에서는 2이고, 서버 환경에서는 10임)을 100으로 늘립니다. 일반적으로 이 값을 애플리케이션에서 사용되는 대략적인 스레드 수로 설정해야 합니다.

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

연결을 열기 전에 연결 제한을 설정합니다.

기타 프로그래밍 언어의 경우 해당 언어의 설명서에서 연결 제한을 설정하는 방법을 확인하세요.

자세한 내용은 [웹 서비스: 동시 연결](/archive/blogs/darrenj/web-services-concurrent-connections) 블로그 게시물을 참조하세요.

### <a name="increase-the-minimum-number-of-threads"></a>최소 스레드 수 늘리기

비동기 작업에서 동기 호출을 함께 사용하는 경우 스레드 풀의 스레드 수를 늘릴 수 있습니다.

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine the right number for your application)  
```

자세한 내용은 [`ThreadPool.SetMinThreads`](/dotnet/api/system.threading.threadpool.setminthreads) 메서드를 참조하세요.

## <a name="unbounded-parallelism"></a>무제한 병렬 처리

병렬 처리는 성능에 매우 유용할 수 있지만, 스레드 수 또는 병렬 처리 요청 수가 제한되지 않는 무제한 병렬 처리를 사용하는 데 주의해야 합니다. 데이터를 업로드하거나 다운로드하거나, 동일한 스토리지 계정의 여러 파티션에 액세스하거나, 동일한 파티션의 여러 항목에 액세스하기 위한 병렬 요청은 제한해야 합니다. 무제한 병렬 처리인 경우 애플리케이션에서 클라이언트 디바이스의 기능 또는 스토리지 계정의 확장성 목표를 초과하여 대기 시간과 제한이 길어질 수 있습니다.

## <a name="client-libraries-and-tools"></a>클라이언트 라이브러리 및 도구

최상의 성능을 위해 항상 Microsoft에서 제공하는 최신 클라이언트 라이브러리와 도구를 사용합니다. Azure Storage 클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 또한 Azure Storage는 PowerShell 및 Azure CLI도 지원합니다. Microsoft는 성능을 고려하여 이러한 클라이언트 라이브러리와 도구를 적극적으로 개발하고, 최신 서비스 버전으로 해당 도구를 최신 상태로 유지하며, 이를 통해 검증된 여러 성능 사례를 내부적으로 처리하고 있습니다. 자세한 내용은 [Azure Storage 참조 설명서](./reference.md)를 참조하세요.

## <a name="handle-service-errors"></a>서비스 오류 처리

서비스에서 요청을 처리할 수 없는 경우 Azure Storage는 오류를 반환합니다. 지정된 시나리오에서 Azure Storage가 반환할 수 있는 오류를 이해하면 성능을 최적화하는 데 도움이 됩니다.

### <a name="timeout-and-server-busy-errors"></a>시간 제한 및 서버 작업 중 오류

확장성 제한에 도달하면 Azure Storage에서 애플리케이션을 제한할 수 있습니다. Azure Storage에서 일시적인 조건으로 인해 요청을 처리하지 못하는 경우도 있습니다. 두 경우 모두 서비스에서 503(`Server Busy`) 또는 500(`Timeout`) 오류를 반환할 수 있습니다. 이러한 오류는 서비스에서 처리량을 높이기 위해 데이터 파티션을 균형 있게 다시 분산시키는 경우에도 발생할 수 있습니다. 클라이언트 애플리케이션은 일반적으로 이러한 오류 중 하나가 발생되는 작업을 다시 시도해야 합니다. 그러나 애플리케이션에서 확장성 목표를 초과하여 Azure Storage에서 애플리케이션을 제한하는 경우 또는 서비스에서 다른 이유로 요청을 처리할 수 없었던 경우에도 적극적인 재시도로 인해 문제가 악화될 수 있습니다. 지수 백오프 재시도 정책을 사용하는 것이 좋으며, 클라이언트 라이브러리는 기본적으로 이 동작으로 설정됩니다. 예를 들어 애플리케이션은 작업을 2초, 4초, 10초, 30초 후에 다시 시도한 다음, 계속 실패하면 작업을 완전히 포기할 수 있습니다. 이렇게 하면 애플리케이션에서 제한으로 이어질 수 있는 동작을 악화시키는 대신 서비스에 대한 부하를 크게 줄입니다.

연결 오류는 제한으로 인해 발생하는 것이 아니라 일시적이므로 즉시 다시 시도할 수 있습니다.

### <a name="non-retryable-errors"></a>다시 시도할 수 없는 오류

클라이언트 라이브러리는 다시 시도할 수 있는 오류와 다시 시도할 수 없는 오류를 인식하여 재시도를 처리합니다. 그러나 Azure Storage REST API를 직접 호출하는 경우에는 다시 시도하지 않아야 하는 오류가 있습니다. 예를 들어 400(`Bad Request`) 오류는 클라이언트 애플리케이션에서 예상되지 않은 형식으로 인해 처리할 수 없는 요청을 보냈음을 나타냅니다. 이 요청을 다시 보내면 매번 동일한 응답이 발생하므로 다시 시도할 필요가 없습니다. Azure Storage REST API를 직접 호출하는 경우 잠재적 오류와 재시도 여부를 알고 있어야 합니다.

Azure Storage 오류 코드에 대한 자세한 내용은 [상태 및 오류 코드](/rest/api/storageservices/status-and-error-codes2)를 참조하세요.

## <a name="disable-nagles-algorithm"></a>Nagle의 알고리즘 사용 안 함

Nagle 알고리즘은 네트워크 성능을 개선하기 위한 수단으로 TCP/IP 네트워크에서 광범위하게 구현됩니다. 그러나 대화형 작업을 많이 수행하는 환경 등 일부 상황에서는 이 알고리즘이 적합하지 않습니다. Nagle의 알고리즘은 Azure Table Storage에 대한 요청 성능에 부정적인 영향을 미치므로 가능하면 이를 사용하지 않도록 설정해야 합니다.

## <a name="message-size"></a>메시지 크기

메시지 크기가 늘어날수록 큐의 성능과 확장성이 줄어듭니다. 수신자에 필요한 정보만 메시지에 배치합니다.

## <a name="batch-retrieval"></a>일괄 처리 검색

단일 작업에서 큐의 메시지를 32개까지 검색할 수 있습니다. 일괄 처리 검색은 클라이언트 애플리케이션의 왕복 횟수를 줄일 수 있으며, 이는 대기 시간이 긴 모바일 디바이스와 같은 환경에서 특히 유용합니다.

## <a name="queue-polling-interval"></a>큐 폴링 간격

대부분의 애플리케이션은 큐에서 메시지를 폴링하는데 이는 해당 애플리케이션에 대한 트랜잭션의 최대 소스 중 하나일 수 있습니다. 폴링 간격은 현명하게 선택하세요. 너무 자주 폴링하면 애플리케이션이 큐의 확장성 목표에 근접할 수 있습니다. 그러나 0.01달러(작성 시점의 경우)로 200,000개의 트랜잭션을 처리하는 단일 프로세서가 1초에 한 번씩 폴링할 경우 한 달에 15센트 미만이 소요되므로 일반적으로 비용은 폴링 간격을 선택하는 데 영향을 미치는 요소가 아닙니다.

최신 비용 정보는 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.

## <a name="perform-an-update-message-operation"></a>업데이트 메시지 작업 수행

메시지 업데이트 작업을 수행하여 표시 안 함 시간 제한을 늘리거나 메시지의 상태 정보를 업데이트할 수 있습니다. 이 접근 방식은 작업의 각 단계가 완료될 때 작업을 한 큐에서 다음 큐로 전달하는 워크플로를 사용하는 것보다 더 효율적일 수 있습니다. 단계가 완료될 때마다 작업의 다음 단계에 대한 메시지를 큐에 다시 넣는 대신, 애플리케이션에서 작업 상태를 메시지에 저장한 후에 작업을 계속할 수 있습니다. 각 메시지 업데이트 작업은 확장성 목표의 계산에 포함됩니다.

## <a name="application-architecture"></a>애플리케이션 아키텍처

애플리케이션 아키텍처를 확장할 수 있게 하려면 큐를 사용합니다. 다음 목록에는 큐를 사용하여 애플리케이션의 확장성을 높이는 몇 가지 방법이 나와 있습니다.

- 큐를 사용하여 애플리케이션에서 워크로드를 처리하고 원활하게 진행하기 위해 작업 백로그를 만들 수 있습니다. 예를 들어 업로드된 이미지 크기를 조정하는 등 프로세서를 많이 사용하는 작업을 수행하기 위한 사용자의 요청을 큐에 대기시킬 수 있습니다.
- 큐를 사용하여 애플리케이션의 각 부분을 독립적으로 확장 가능하도록 분리할 수 있습니다. 예를 들어 웹 프런트 엔드에서 나중에 분석 및 스토리지하기 위해 사용자의 설문 조사 결과를 큐에 대기할 수 있습니다. 필요한 경우 큐 데이터를 처리하기 위해 작업자 역할 인스턴스를 더 추가할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Queue Storage의 확장성 및 성능 목표](scalability-targets.md)
- [표준 스토리지 계정의 확장성 및 성능 목표](../common/scalability-targets-standard-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
- [상태 및 오류 코드](/rest/api/storageservices/Status-and-Error-Codes2)

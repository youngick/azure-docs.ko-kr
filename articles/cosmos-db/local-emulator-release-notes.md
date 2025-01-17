---
title: Azure Cosmos DB Emulator 다운로드 및 릴리스 정보
description: 다양한 버전에 대한 Azure Cosmos DB Emulator 릴리스 정보를 가져오고 정보를 다운로드합니다.
ms.service: cosmos-db
ms.topic: conceptual
author: milismsft
ms.author: adrianmi
ms.date: 09/21/2020
ms.openlocfilehash: 23f85fa69224d78d748e6fc94436fd08fa6d971f
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104586015"
---
# <a name="azure-cosmos-db-emulator---release-notes-and-download-information"></a>Azure Cosmos DB Emulator - 릴리스 정보 및 다운로드 정보
[!INCLUDE[appliesto-all-apis](includes/appliesto-all-apis.md)]

이 문서에서는 Azure Cosmos DB Emulator 릴리스 정보와 각 릴리스의 기능 업데이트 목록을 알아봅니다. 또한 다운로드 및 사용할 수 있는 에뮬레이터의 최신 버전도 나와 있습니다.

## <a name="download"></a>다운로드

| |링크 |
|---------|---------|
|**MSI 다운로드**|[Microsoft 다운로드 센터](https://aka.ms/cosmosdb-emulator)|
|**시작**|[Azure Cosmos DB Emulator를 사용하여 로컬로 개발](local-emulator.md)|

## <a name="release-notes"></a>릴리스 정보

### <a name="21111-22-february-2021"></a>2.11.11(2021년 2월 22일)

 - 이 릴리스는 로컬 데이터 탐색기 콘텐츠를 최신 Azure Portal 버전으로 업데이트합니다.


### <a name="21110-5-january-2021"></a>2.11.10(2021년 1월 5일)

 - 이 릴리스는 로컬 데이터 탐색기 콘텐츠를 최신 Azure Portal 버전으로 업데이트하고 에뮬레이터 사용자가 공용 에뮬레이터의 인증서를 .PEM 파일로 직접 내보낼 수 있는 새로운 공용 옵션인 ‘/ExportPemCert’를 추가합니다.

### <a name="2119-3-december-2020"></a>2.11.9(2020년 12월 3일)

 - 이 릴리스는 Azure Cosmos DB의 최신 기능과 개선 사항을 반영하는 일반 콘텐츠 업데이트 외에도 Azure Cosmos DB 에뮬레이터 기능과 관련된 몇 가지 문제를 해결합니다.
 * 직접 모드 및 Java 클라이언트 애플리케이션을 사용할 때 대량 문서 페이로드 요청이 실패하는 문제를 해결합니다.
 * .NET 기반 애플리케이션을 대상으로 하는 경우 MongoDB 엔드포인트 버전 3.6의 연결 문제를 해결합니다.

### <a name="2118-6-november-2020"></a>2.11.8(2020년 11월 6일)

 - 이 릴리스에는 Cosmos 에뮬레이터 Data Explorer 업데이트가 포함되어 있으며, TLS 1.3 클라이언트가 Data Explorer를 열려고 시도하는 문제를 해결합니다.

### <a name="2116-6-october-2020"></a>2.11.6(2020년 10월 6일)

 - 이 릴리스는 동시에 여러 컨테이너를 만들 수 있는 경우 동시성 관련 문제를 해결합니다. 이러한 경우 에뮬레이터의 데이터가 손상된 상태로 유지되고 에뮬레이터의 엔드포인트에 대한 후속 API 요청이 "서비스 사용 불가" 오류와 함께 실패할 수 있으며 에뮬레이터의 로컬 데이터를 다시 시작하고 재설정해야 할 수 있습니다.

### <a name="2115-23-august-2020"></a>2.11.5(2020년 8월 23일)

이 릴리스에는 다음과 같은 두 개의 새로운 Cosmos 에뮬레이터 시작 옵션이 추가되었습니다. 

* "/EnablePreview" - 에뮬레이터의 미리 보기 기능을 사용하도록 설정합니다. 아직 개발 중인 미리 보기 기능은 CI 및 샘플 작성을 통해 액세스할 수 있습니다.
* "/EnableAadAuthentication" - 에뮬레이터에서 Azure Cosmos 기본 키에 대한 대안으로 사용자 지정 Azure Active Directory 토큰을 허용할 수 있습니다. 이 기능은 아직 개발 중입니다. 특정 역할 할당 및 기타 권한 관련 설정은 현재 지원되지 않습니다.

### <a name="2112-07-july-2020"></a>2.11.2(2020년 7월 7일)

- 이 릴리스는 Cosmos 에뮬레이터 문제를 해결할 때 필요한 ETL 추적을 수집하는 방법을 변경합니다. 이제 ETL 기반 추적을 캡처하는 기본 도구는 WPR(Windows Performance Runtime 도구)이며, 이전 LOGMAN 기반 캡처는 더 이상 사용되지 않습니다. 최신 Windows 보안 업데이트가 Cosmos 에뮬레이터를 통해 실행될 때 LOGMAN 작동 방식에 예기치 않은 영향을 주기 때문에 이러한 변경이 부분적으로 필요합니다.

### <a name="2111-10-june-2020"></a>2.11.1(2020년 6월 10일)

- 이 릴리스는 에뮬레이터 데이터 탐색기와 관련된 몇 가지 버그를 수정합니다. 웹 브라우저를 통해 에뮬레이터 데이터 탐색기를 사용할 때 Cosmos 에뮬레이터 엔드포인트에 연결하지 못하고 데이터베이스 또는 컨테이너 생성과 같은 모든 관련 작업에 오류가 발생하는 경우가 있습니다. 수정된 두 번째 문제는 데이터 탐색기 업로드 동작을 사용하여 JSON 파일에서 항목을 만드는 것과 관련이 있습니다.

### <a name="2110"></a>2.11.0

- 이 릴리스에서는 자동 크기 조정 프로비저닝된 처리량에 대한 지원이 도입되었습니다. 이러한 새로운 기능에는 사용자 지정 최대 프로비저닝된 처리량 수준을 요청 단위(RU/s)로 설정하고, 기존 데이터베이스 및 컨테이너에서 자동 크기 조정을 사용하고, Azure Cosmos DB SDK를 통해 프로그래밍 방식으로 지원할 수 있는 기능이 포함됩니다.
- 내부 오류 상태 코드 500으로 인해 에뮬레이터가 실패했으므로 대량의 문서(1GB 초과)를 통해 쿼리하는 동안 문제를 해결합니다.

### <a name="292"></a>2.9.2

- 이 릴리스는 MongoDb 엔드포인트 버전 3.2에 대한 지원을 사용하도록 설정하는 동안 버그를 수정합니다. LOGMAN 대신 WPR을 사용하여 문제 해결을 위한 ETL 추적 생성 지원도 추가합니다.

### <a name="291"></a>2.9.1

- 이 릴리스는 쿼리 API 지원의 몇 가지 문제를 해결하고 Windows Server 2012와 같은 이전 OS와의 호환성을 복원합니다.

### <a name="290"></a>2.9.0

- 이 릴리스에는 일관성을 일관된 접두사로 설정하고 사용자 및 사용 권한의 최대 제한을 늘리는 옵션이 추가되었습니다.

### <a name="272"></a>2.7.2

- 이 릴리스에는 MongoDB 버전 3.6 서버 지원이 Cosmos 에뮬레이터에 추가되었습니다. 3\.6 버전의 서비스를 대상으로 하는 MongoDB 엔드포인트를 시작하려면 "/EnableMongoDBEndpoint=3.6" 옵션을 사용하여 관리자 명령줄에서 에뮬레이터를 시작합니다.

### <a name="270"></a>2.7.0

- 이 릴리스에서는 .NET 코어 또는 x86 .NET 기반 클라이언트를 사용할 때 사용자가 에뮬레이터에서 SQL API 계정에 대해 쿼리를 실행할 수 없도록 하는 회귀를 수정합니다.

### <a name="246"></a>2.4.6

- 이 릴리스에서는 [Azure Cosmos DB Emulator를 사용하여 로컬로 개발](local-emulator.md)에 설명된 예외가 포함된 2019년 7월 현재 Azure Cosmos 서비스의 기능과 패리티를 제공합니다. 또한 직접 모드 연결을 사용하는 SDK 클라이언트에 대한 명령줄 및 내부 IP 주소 재정의를 통해 호출될 때 에뮬레이터 종료와 관련된 몇 가지 버그를 수정합니다.

### <a name="243"></a>2.4.3

- 기본적으로 MongoDB 서비스 시작은 사용하지 않도록 설정되어 있습니다. SQL 엔드포인트만 기본값으로 사용됩니다. 사용자는 에뮬레이터의 "/EnableMongoDbEndpoint" 명령줄 옵션을 사용하여 수동으로 엔드포인트를 시작해야 합니다. 이제 Gremlin, Cassandra 및 Table 등 모든 기타 서비스 엔드포인트와 마찬가지입니다.
- “/AllowNetworkAccess”를 시작할 때 Gremlin, Cassandra 및 Table 엔드포인트가 외부 클라이언트의 요청을 제대로 처리하지 않는 에뮬레이터 버그를 수정했습니다.
- 방화벽 규칙 설정에 직접 연결 포트를 추가합니다.

### <a name="240"></a>2.4.0

- Pulse 클라이언트와 같은 네트워크 모니터링 앱이 호스트 컴퓨터에 있는 경우 시작하지 못하는 에뮬레이터 문제를 해결했습니다.

---
title: 파일 포함
description: 포함 파일
services: azure-communication-services
author: tomaschladek
manager: nmurav
ms.service: azure-communication-services
ms.subservice: azure-communication-services
ms.date: 03/10/2021
ms.topic: include
ms.custom: include file
ms.author: tchladek
ms.openlocfilehash: a0f8744061853e8bd81d3435c1f007e96a7d5783
ms.sourcegitcommit: 4bda786435578ec7d6d94c72ca8642ce47ac628a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103495326"
---
## <a name="prerequisites"></a>사전 요구 사항

- 활성 구독이 있는 Azure 계정. [체험 계정을 만듭니다](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- 운영 체제에 대한 최신 버전의 [.NET Core 클라이언트 라이브러리](https://dotnet.microsoft.com/download/dotnet-core)
- 활성 Communication Services 리소스 및 연결 문자열 [Communication Services 리소스를 만듭니다](../create-communication-resource.md).

## <a name="setting-up"></a>설치

### <a name="create-a-new-c-application"></a>새 C# 애플리케이션 만들기

콘솔 창(예: cmd, PowerShell 또는 Bash)에서 `dotnet new` 명령을 사용하여 `AccessTokensQuickstart`라는 새 콘솔 앱을 만듭니다. 이 명령은 **Program.cs** 라는 원본 파일 하나만 들어 있는 간단한 "Hello World" C# 프로젝트를 만듭니다.

```console
dotnet new console -o AccessTokensQuickstart
```

디렉터리를 새로 만든 앱 폴더로 변경하고 `dotnet build` 명령을 사용하여 애플리케이션을 컴파일합니다.

```console
cd AccessTokensQuickstart
dotnet build
```

### <a name="install-the-package"></a>패키지 설치

애플리케이션 디렉터리에 있는 동안 `dotnet add package` 명령을 사용하여 .NET 패키지용 Azure Communication Services ID 라이브러리를 설치합니다.

```console
dotnet add package Azure.Communication.Identity --version 1.0.0-beta.5
```

### <a name="set-up-the-app-framework"></a>앱 프레임워크 설정

프로젝트 디렉터리에서 다음을 수행합니다.

1. 텍스트 편집기에서 **Program.cs** 파일 열기
1. `Azure.Communication.Identity` 네임스페이스를 포함하는 `using` 지시문 추가
1. 비동기 코드를 지원하도록 `Main` 메서드 선언 업데이트

시작하려면 다음 코드를 사용합니다.

```csharp
using System;
using Azure.Communication;
using Azure.Communication.Identity;

namespace AccessTokensQuickstart
{
    class Program
    {
        static async System.Threading.Tasks.Task Main(string[] args)
        {
            Console.WriteLine("Azure Communication Services - Access Tokens Quickstart");

            // Quickstart code goes here
        }
    }
}
```
## <a name="authenticate-the-client"></a>클라이언트 인증

연결 문자열로 `CommunicationIdentityClient`를 초기화합니다. 아래 코드는 `COMMUNICATION_SERVICES_CONNECTION_STRING`이라는 환경 변수에서 리소스에 대한 연결 문자열을 검색합니다. [리소스의 연결 문자열을 관리](../create-communication-resource.md#store-your-connection-string)하는 방법을 알아봅니다.

`Main` 메서드에 다음 코드를 추가합니다.

```csharp
// This code demonstrates how to fetch your connection string
// from an environment variable.
string connectionString = Environment.GetEnvironmentVariable("COMMUNICATION_SERVICES_CONNECTION_STRING");
var client = new CommunicationIdentityClient(connectionString);
```

또는 엔드포인트 및 액세스 키를 구분할 수 있습니다.
```csharp
// This code demonstrates how to fetch your endpoint and access key
// from an environment variable.
string endpoint = Environment.GetEnvironmentVariable("COMMUNICATION_SERVICES_ENDPOINT");
string accessKey = Environment.GetEnvironmentVariable("COMMUNICATION_SERVICES_ACCESSKEY");
var client = new CommunicationIdentityClient(new Uri(endpoint), new AzureKeyCredential(accessKey));
```

관리 ID가 설정된 경우([관리 ID 사용](../managed-identity.md) 참조) 관리 ID로 인증할 수도 있습니다.
```csharp
TokenCredential tokenCredential = new DefaultAzureCredential();
var client = new CommunicationIdentityClient(endpoint, tokenCredential);
```

## <a name="create-an-identity"></a>ID 만들기

Azure Communication Services는 경량 ID 디렉터리를 유지 관리합니다. `createUser` 메서드를 사용하여 고유한 `Id`로 디렉터리에 새 항목을 만듭니다. 애플리케이션의 사용자에게 매핑하여 수신된 ID를 저장합니다. 예를 들어 애플리케이션 서버의 데이터베이스에 저장합니다. ID는 나중에 액세스 토큰을 발급하는 데 필요합니다.

```csharp
var identityResponse = await client.CreateUserAsync();
var identity = identityResponse.Value;
Console.WriteLine($"\nCreated an identity with ID: {identity.Id}");
```

## <a name="issue-identity-access-tokens"></a>ID 액세스 토큰 발급

`GetToken` 메서드를 사용하여 이미 존재하는 Communication Services ID에 대한 액세스 토큰을 발급합니다. 매개 변수 `scopes`는 이 액세스 토큰에 권한을 부여하는 기본 형식 세트를 정의합니다. [지원되는 작업 목록](../../concepts/authentication.md)을 참조하세요. 매개 변수 `communicationUser`의 새 인스턴스는 Azure Communication Service ID의 문자열 표현에 따라 구성될 수 있습니다.

```csharp
// Issue an access token with the "voip" scope for an identity
var tokenResponse = await client.GetTokenAsync(identity, scopes: new [] { CommunicationTokenScope.VoIP });
var token =  tokenResponse.Value.Token;
var expiresOn = tokenResponse.Value.ExpiresOn;
Console.WriteLine($"\nIssued an access token with 'voip' scope that expires at {expiresOn}:");
Console.WriteLine(token);
```

액세스 토큰은 다시 발급해야 하는 단기 자격 증명입니다. 이렇게 하지 않으면 애플리케이션의 사용자 환경이 중단될 수 있습니다. `expiresOn` 응답 속성은 액세스 토큰의 수명을 나타냅니다.

## <a name="create-an-identity-and-issue-an-access-token-within-the-same-request"></a>ID를 만들고 동일한 요청 내에서 액세스 토큰을 발급합니다.

`CreateUserAndTokenAsync` 메서드를 사용하여 Communication Services ID를 만들고 이에 대한 액세스 토큰을 발급합니다. 매개 변수 `scopes`는 이 액세스 토큰에 권한을 부여하는 기본 형식 세트를 정의합니다. [지원되는 작업 목록](../../concepts/authentication.md)을 참조하세요.

```csharp
// Issue an identity and an access token with the "voip" scope for the new identity
var identityAndTokenResponse = await client.CreateUserAndTokenAsync(scopes: new[] { CommunicationTokenScope.VoIP });
var identity = identityAndTokenResponse.Value.User;
var token = identityAndTokenResponse.Value.AccessToken.Token;
var expiresOn = identityAndTokenResponse.Value.AccessToken.ExpiresOn;

Console.WriteLine($"\nCreated an identity with ID: {identity.Id}");
Console.WriteLine($"\nIssued an access token with 'voip' scope that expires at {expiresOn}:");
Console.WriteLine(token);
```

## <a name="refresh-access-tokens"></a>액세스 토큰 새로 고침

액세스 토큰을 새로 고치려면 `CommunicationUserIdentifier` 개체의 인스턴스를 `GetTokenAsync`에 전달합니다. 이 `Id`를 저장했고 새 `CommunicationUserIdentifier`를 만들어야 하는 경우 다음과 같이 저장된 `Id`를 `CommunicationUserIdentifier` 생성자에 전달하면 됩니다.

```csharp
// In this example, userId is a string containing the Id property of a previously-created CommunicationUser
var identityToRefresh = new CommunicationUserIdentifier(userId);
var tokenResponse = await client.GetTokenAsync(identityToRefresh, scopes: new [] { CommunicationTokenScope.VoIP });
```

## <a name="revoke-access-tokens"></a>액세스 토큰 취소

경우에 따라 액세스 토큰을 명시적으로 취소할 수 있습니다. 예를 들어 애플리케이션의 사용자가 서비스에 인증하는 데 사용하는 암호를 변경하는 경우입니다. 메서드 `RevokeTokensAsync`는 ID에 발급된 모든 활성 액세스 토큰을 무효화합니다.

```csharp
await client.RevokeTokensAsync(identity);
Console.WriteLine($"\nSuccessfully revoked all access tokens for identity with ID: {identity.Id}");
```

## <a name="delete-an-identity"></a>ID 삭제

ID를 삭제하면 모든 활성 액세스 토큰이 취소되고 ID에 대한 액세스 토큰을 발급할 수 없게 됩니다. 또한 ID와 연결된 모든 지속형 콘텐츠를 제거합니다.

```csharp
await client.DeleteUserAsync(identity);
Console.WriteLine($"\nDeleted the identity with ID: {identity.Id}");
```

## <a name="run-the-code"></a>코드 실행

`dotnet run` 명령을 사용하여 애플리케이션 디렉터리에서 애플리케이션을 실행합니다.

```console
dotnet run
```

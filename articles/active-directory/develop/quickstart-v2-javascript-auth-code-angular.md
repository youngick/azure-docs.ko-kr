---
title: '빠른 시작: 인증 코드를 사용하여 JavaScript Angular SPA(단일 페이지 앱)에서 사용자를 로그인하고 Microsoft Graph 호출 | Azure'
titleSuffix: Microsoft identity platform
description: 이 빠른 시작에서는 JavaScript Angular SPA(단일 페이지 애플리케이션)에서 인증 코드 흐름을 사용하고 Microsoft Graph를 호출하여 개인 계정, 회사 및 학교 계정의 사용자에 로그인하는 방법을 알아봅니다.
services: active-directory
author: j-mantu
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 01/14/2021
ms.author: jamesmantu
ms.custom: aaddev, scenarios:getting-started, languages:JavaScript, devx-track-js
ms.openlocfilehash: 1d5fc097be188c820f9be15594f4bb382754b849
ms.sourcegitcommit: 94c3c1be6bc17403adbb2bab6bbaf4a717a66009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2021
ms.locfileid: "103224931"
---
# <a name="quickstart-sign-in-and-get-an-access-token-in-an-angular-spa-using-the-auth-code-flow"></a>빠른 시작: 인증 코드 흐름을 사용하여 Angular SPA에 로그인하고 액세스 토큰을 가져옵니다.

이 빠른 시작에서는 인증 코드 흐름을 사용하여 JavaScript Angular SPA(단일 페이지 애플리케이션)에서 사용자를 로그인하고 Microsoft Graph를 호출할 수 있는 방법을 보여주는 코드 샘플을 다운로드하고 실행합니다. 코드 샘플은 Microsoft Graph API 또는 웹 API를 호출하기 위한 액세스 토큰을 가져오는 방법을 보여줍니다. 

자세한 내용은 [샘플 작동 방식](#how-the-sample-works)을 참조하세요.

이 빠른 시작에서는 인증 코드 흐름과 함께 MSAL Angular v2를 사용합니다. 암시적 흐름과 함께 MSAL Angular 1.x를 사용하는 유사한 빠른 시작은 [빠른 시작: JavaScript 단일 페이지 앱에서 사용자 로그인](./quickstart-v2-angular.md)을 참조하세요.

> [!IMPORTANT]
> MSAL Angular v2 [!INCLUDE [PREVIEW BOILERPLATE](../../../includes/active-directory-develop-preview.md)]

## <a name="prerequisites"></a>필수 구성 요소

* Azure 구독 - [체험용 Azure 구독 만들기](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
* [Node.JS](https://nodejs.org/en/download/)
* [Visual Studio Code](https://code.visualstudio.com/download) 또는 다른 코드 편집기

> [!div renderon="docs"]
> ## <a name="register-and-download-your-quickstart-application"></a>빠른 시작 애플리케이션 등록 및 다운로드
> 빠른 시작 애플리케이션을 시작하려면 다음 옵션 중 하나를 사용합니다.
>
> ### <a name="option-1-express-register-and-auto-configure-your-app-and-then-download-your-code-sample"></a>옵션 1(Express): 앱을 등록하고 자동 구성한 다음, 코드 샘플 다운로드
>
> 1. <a href="https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade/quickStartType/JavascriptSpaQuickstartPage/sourceType/docs" target="_blank">Azure Portal - 앱 등록</a> 빠른 시작 환경으로 이동합니다.
> 1. 애플리케이션의 이름을 입력합니다.
> 1. **지원되는 계정 유형** 아래에서 **모든 조직 디렉터리의 계정 및 개인 Microsoft 계정** 을 선택합니다.
> 1. **등록** 을 선택합니다.
> 1. 빠른 시작 창으로 이동하여 지침에 따라 새 애플리케이션을 다운로드하고 자동으로 구성합니다.
>
> ### <a name="option-2-manual-register-and-manually-configure-your-application-and-code-sample"></a>옵션 2(수동): 애플리케이션 및 코드 샘플을 등록하고 수동으로 구성
>
> #### <a name="step-1-register-your-application"></a>1단계: 애플리케이션 등록
>
> 1. <a href="https://portal.azure.com/" target="_blank">Azure Portal</a>에 로그인합니다.
> 1. 여러 테넌트에 액세스할 수 있는 경우 위쪽 메뉴의 **디렉터리 + 구독** 필터 :::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false":::를 사용하여 애플리케이션을 등록하려는 테넌트를 선택합니다.
> 1. **Azure Active Directory** 를 검색하고 선택합니다.
> 1. **관리** 아래에서 **앱 등록** > **새 등록** 을 선택합니다.
> 1. 애플리케이션의 **이름** 을 입력합니다. 이 이름은 앱의 사용자에게 표시될 수 있으며 나중에 변경할 수 있습니다.
> 1. **지원되는 계정 유형** 아래에서 **모든 조직 디렉터리의 계정 및 개인 Microsoft 계정** 을 선택합니다.
> 1. **등록** 을 선택합니다. 나중에 사용할 수 있도록 앱 **개요** 페이지에서 **애플리케이션(클라이언트) ID** 값을 기록해 둡니다.
> 1. **관리** 에서 **인증** 을 선택합니다.
> 1. **플랫폼 구성** 에서 **플랫폼 추가** 를 선택합니다. 열린 창에서 **단일 페이지 애플리케이션** 을 선택합니다.
> 1. **리디렉션 URI** 값을 `http://localhost:4200/`으로 설정합니다. 이는 로컬 머신에서 수신하는 기본 포트 NodeJS입니다. 성공적으로 사용자를 인증한 후에 이 URl에 인증 응답을 반환합니다. 
> 1. **구성** 을 선택하여 변경 내용을 적용합니다.
> 1. **플랫폼 구성** 에서 **단일 페이지 애플리케이션** 을 확장합니다.
> 1. **권한 부여 형식** 에서 ![이미 구성](media/quickstart-v2-javascript/green-check.png)된 리디렉션 URI가 PKCE를 사용하는 권한 부여 코드 흐름에 적합한지 확인합니다.

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-1-configure-your-application-in-the-azure-portal"></a>1단계: Azure Portal에서 애플리케이션 구성
> 이 빠른 시작의 코드 샘플이 작동하려면 `http://localhost:4200/`의 **리디렉션 URI** 를 추가합니다.
> > [!div renderon="portal" id="makechanges" class="nextstepaction"]
> > [이러한 변경 내용 적용]()
>
> > [!div id="appconfigured" class="alert alert-info"]
> > ![이미 구성됨](media/quickstart-v2-javascript/green-check.png) 이러한 특성을 사용하여 애플리케이션을 구성합니다.

 #### <a name="step-2-download-the-project"></a>2단계: 프로젝트를 다운로드합니다.

> [!div renderon="docs"]
> Node.js를 사용하여 웹 서버로 프로젝트를 실행하려면 [주요 프로젝트 파일을 다운로드](https://github.com/Azure-Samples/ms-identity-javascript-angular-spa/archive/main.zip)합니다.

> [!div renderon="portal" class="sxs-lookup"]
> Node.js를 사용하여 웹 서버에서 프로젝트 실행

> [!div renderon="portal" class="sxs-lookup" id="autoupdate" class="nextstepaction"]
> [코드 샘플 다운로드](https://github.com/Azure-Samples/ms-identity-javascript-angular-spa/archive/main.zip)

> [!div renderon="docs"]
> #### <a name="step-3-configure-your-javascript-app"></a>3단계: JavaScript 앱 구성
>
> *src* 폴더에서 *app* 폴더를 연 다음, *app.module.ts* 파일을 열고 `auth` 개체에서 `clientID`, `authority`, `redirectUri` 값을 업데이트합니다.
>
> ```javascript
> // MSAL instance to be passed to msal-angular
> export function MSALInstanceFactory(): IPublicClientApplication {
>   return new PublicClientApplication({
>     auth: {
>       clientId: 'Enter_the_Application_Id_Here',
>       authority: 'Enter_the_Cloud_Instance_Id_HereEnter_the_Tenant_Info_Here',
>       redirectUri: 'Enter_the_Redirect_Uri_Here'
>     },
>     cache: {
>       cacheLocation: BrowserCacheLocation.LocalStorage,
>       storeAuthStateInCookie: isIE, // set to true for IE 11
>     },
>   });
> }
> ```

> [!div renderon="portal" class="sxs-lookup"]
> > [!NOTE]
> > `Enter_the_Supported_Account_Info_Here`

> [!div renderon="docs"]
>
> 여기에 설명한 대로 `auth` 섹션에서 값을 수정합니다.
>
> - `Enter_the_Application_Id_Here`는 등록한 애플리케이션의 **애플리케이션(클라이언트) ID** 입니다.
>
>    **애플리케이션(클라이언트) ID** 값을 찾으려면 Azure Portal에서 앱 등록의 **개요** 페이지로 이동합니다.
> - `Enter_the_Cloud_Instance_Id_Here`는 Azure 클라우드의 인스턴스입니다. 주 또는 글로벌 Azure 클라우드의 경우 `https://login.microsoftonline.com/`을 입력합니다. **국가별** 클라우드(예제: 중국)의 경우 [국가별 클라우드](authentication-national-cloud.md)를 참조하세요.
> - `Enter_the_Tenant_info_here`는 다음 중 하나로 설정됩니다.
>   - 애플리케이션에서 *이 조직 디렉터리의 계정* 을 지원하는 경우 이 값을 **테넌트 ID** 또는 **테넌트 이름** 으로 바꿉니다. 예들 들어 `contoso.microsoft.com`입니다.
>
>    **디렉터리(테넌트) ID** 값을 찾으려면 Azure Portal에서 앱 등록의 **개요** 페이지로 이동합니다.
>   - 애플리케이션에서 *모든 조직 디렉터리의 계정* 을 지원하는 경우 이 값을 `organizations`로 바꾸세요.
>   - 애플리케이션에서 *모든 조직 디렉터리의 계정 및 개인 Microsoft 계정* 을 지원하는 경우 이 값을 `common`으로 바꿉니다. **이 빠른 시작** 에 대해 `common`을 사용합니다.
>   - *개인 Microsoft 계정만* 지원하도록 제한하려면 이 값을 `consumers`로 바꿉니다.
>
>    **지원되는 계정 유형** 값을 찾으려면 Azure Portal에서 앱 등록의 **개요** 페이지로 이동합니다.
> - `Enter_the_Redirect_Uri_Here`은 `http://localhost:4200/`입니다.
>
> 기본(글로벌) Azure 클라우드를 사용하는 경우 *app.module.ts* 의 `authority` 값은 다음과 비슷해야 합니다.
>
> ```javascript
> authority: "https://login.microsoftonline.com/common",
> ```
>

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-3-your-app-is-configured-and-ready-to-run"></a>3단계: 앱이 구성되었고 실행할 준비가 되었습니다.
> 앱 속성 값을 사용하여 프로젝트를 구성했습니다.

> [!div renderon="docs"]
>
> 동일한 파일에서 아래로 스크롤하고 `graphMeEndpoint`를 업데이트합니다. 
> - `Enter_the_Graph_Endpoint_Herev1.0/me` 문자열을 `https://graph.microsoft.com/v1.0/me`로 바꿉니다.
> - `Enter_the_Graph_Endpoint_Herev1.0/me`는 API 호출이 수행될 엔드포인트입니다. 기본(글로벌) Microsoft Graph API 서비스의 경우 `https://graph.microsoft.com/`(후행 슬래시 포함)을 입력합니다. 자세한 내용은 [설명서](/graph/deployments)를 참조하세요.
>
>
> ```javascript
> export function MSALInterceptorConfigFactory(): MsalInterceptorConfiguration {
>   const protectedResourceMap = new Map<string, Array<string>>();
>   protectedResourceMap.set('Enter_the_Graph_Endpoint_Herev1.0/me', ['user.read']);
>
>   return {
>     interactionType: InteractionType.Redirect,
>     protectedResourceMap
>   };
> }
> ```
>
>
 #### <a name="step-4-run-the-project"></a>4단계: 프로젝트 실행

Node.js를 사용하여 웹 서버에서 프로젝트 실행:

1. 서버를 시작하려면 프로젝트의 디렉터리 내에서 다음 명령을 실행합니다.
    ```console
    npm install
    npm start
    ```
1. [https://www.microsoft.com]\(`http://localhost:4200/`) 로 이동합니다.

1. **로그인** 을 선택하여 로그인 프로세스를 시작한 다음, Microsoft Graph API를 호출합니다.

    사용자가 처음으로 로그인하면 애플리케이션이 사용자 프로필에 액세스하고 로그인할 수 있도록 동의하라는 메시지가 표시됩니다. 성공적으로 로그인한 후 **프로필** 단추를 클릭하여 페이지에 사용자 정보를 표시합니다.

## <a name="more-information"></a>자세한 정보

### <a name="how-the-sample-works"></a>샘플 작동 방법

![단일 페이지 애플리케이션의 인증 코드 흐름을 보여주는 다이어그램.](media/quickstart-v2-javascript-auth-code/diagram-01-auth-code-flow.png)

### <a name="msaljs"></a>msal.js

MSAL.js 라이브러리는 사용자를 로그인하고 Microsoft ID 플랫폼으로 보호되는 API 액세스에 사용되는 토큰을 요청합니다. 

Node.js가 설치된 경우 Node.js 패키지 관리자(npm)를 사용하여 최신 버전을 다운로드할 수 있습니다.

```console
npm install @azure/msal-browser @azure/msal-angular@2
```

## <a name="next-steps"></a>다음 단계

vanilla JavaScript를 사용하여 인증 코드 흐름 애플리케이션을 빌드하는 방법에 대한 자세한 단계별 가이드는 다음 자습서를 참조하세요.

> [!div class="nextstepaction"]
> [MS Graph에 로그인하고 호출하는 자습서](./tutorial-v2-javascript-auth-code.md)
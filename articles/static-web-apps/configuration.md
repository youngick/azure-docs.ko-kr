---
title: Azure Static Web Apps 구성
description: Azure Static Web Apps의 경로를 구성하고, 보안 규칙을 적용하고, 전역 설정을 지정하는 방법을 알아봅니다.
services: static-web-apps
author: craigshoemaker
ms.service: static-web-apps
ms.topic: conceptual
ms.date: 02/18/2021
ms.author: cshoe
ms.openlocfilehash: 324a8e75488d74fc6aa52e499b8dde616cd9beb5
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102034050"
---
# <a name="configure-azure-static-web-apps"></a>Azure Static Web Apps 구성

Azure Static Web Apps의 구성은 _staticwebapp.config.json_ 파일에 정의되어 있으며, 이 파일은 다음 설정을 제어합니다.

- 라우팅
- 인증
- 권한 부여
- 대체(fallback) 규칙
- HTTP 응답 재정의
- 글로벌 HTTP 헤더 정의
- 사용자 지정 MIME 형식

## <a name="file-location"></a>파일 위치

_staticwebapp.config.json_ 의 권장 위치는 [워크플로 파일](./github-actions-workflow.md)에서 `app_location`으로 설정된 폴더입니다. 하지만 애플리케이션 소스 코드 폴더 내부의 모든 위치에 파일을 배치할 수 있습니다.

자세한 내용은 [예제 구성](#example-configuration-file) 파일을 참조하세요.

> [!IMPORTANT]
> _staticwebapp.config.json_ 파일이 있는 경우 [ _routes.json_ 파일](./routes.md)은 무시됩니다.

## <a name="routes"></a>경로

경로 규칙을 통해 웹에서 애플리케이션에 액세스할 수 있도록 허용하는 URL 패턴을 정의할 수 있습니다. 경로는 라우팅 규칙의 배열로 정의됩니다. 사용 예제는 [예제 구성 파일](#example-configuration-file)을 참조하세요.

- 규칙은 `routes` 배열에 표시되는 순서대로 실행됩니다.
- 규칙 평가는 첫 번째 일치 항목에서 멈추고 라우팅 규칙은 서로 연결되지 않습니다.
- 사용자 지정 역할 이름을 완전히 제어할 수 있습니다.
  - [`anonymous`](./authentication-authorization.md) 및 [`authenticated`](./authentication-authorization.md)를 포함하는 몇 가지 기본 역할 이름이 제공됩니다.

라우팅은 인증(사용자 식별) 및 권한 부여(사용자에게 기능 할당) 개념과 중복되는 부분이 상당히 많습니다. 이 문서와 함께 [인증 및 권한 부여](authentication-authorization.md) 가이드를 참조하세요.

정적 콘텐츠의 기본 파일은 *index.html* 파일입니다.

## <a name="defining-routes"></a>경로 정의

각 규칙은 하나 이상의 선택적 규칙 속성과 함께 경로 패턴으로 구성됩니다. 사용 예제는 [예제 구성 파일](#example-configuration-file)을 참조하세요.

| 규칙 속성  | 필수 | 기본값 | 주석                                                      |
| -------------- | -------- | ------------- | ------------------------------------------------------------ |
| `route`        | 예      | 해당 없음          | 호출자가 요청한 경로 패턴입니다.<ul><li>[와일드카드](#wildcards)는 경로 경로(route path)의 끝에서 지원됩니다.<ul><li>예를 들어 경로 _admin/\*_ 은 _admin_ 경로 아래에 있는 경로와 일치합니다.</ul></ul>|
| `rewrite`        | 예       | 해당 없음          | 요청에서 반환된 파일 또는 경로를 정의합니다.<ul><li>`redirect` 규칙과 함께 사용할 수 없습니다.<li>다시 쓰기 규칙은 브라우저의 위치를 변경하지 않습니다.<li>값은 앱의 루트에 대한 상대 경로여야 합니다.</ul>  |
| `redirect`        | 예       | 해당 없음          | 요청의 파일 또는 경로 리디렉션 대상을 정의합니다.<ul><li>`rewrite` 규칙과 함께 사용할 수 없습니다.<li>리디렉션 규칙은 브라우저의 위치를 변경합니다.<li>기본 응답 코드는 [`302`](https://developer.mozilla.org/docs/Web/HTTP/Status/302)(임시 리디렉션)지만 [`301`](https://developer.mozilla.org/docs/Web/HTTP/Status/301)(영구 리디렉션)로 재정의할 수 있습니다.</ul> |
| `allowedRoles` | 예       | 익명     | 경로에 액세스하는 데 필요한 역할 이름 목록을 정의합니다. <ul><li>유효한 문자에는 `a-z`, `A-Z`, `0-9` 및 `_`가 포함됩니다.<li>기본 제공 역할 [`anonymous`](./authentication-authorization.md)는 인증되지 않은 모든 사용자에게 적용됩니다.<li>기본 제공 역할 [`authenticated`](./authentication-authorization.md)는 로그인한 사용자에게 적용됩니다.<li>사용자는 하나 이상의 역할에 속해야 합니다.<li>역할은 _OR_ 기준으로 일치합니다.<ul><li>사용자가 나열된 역할 중 하나에 있는 경우 액세스 권한이 부여됩니다.</ul><li>개별 사용자는 [초대](authentication-authorization.md)를 통해 역할에 연결됩니다.</ul> |
| `headers`<a id="route-headers"></a> | 예 | 해당 없음 | 응답에 추가된 [HTTP 헤더](https://developer.mozilla.org/docs/Web/HTTP/Headers) 세트입니다. <ul><li>경로 관련 헤더가 응답의 글로벌 헤더와 동일한 경우 경로 관련 헤더가 [`globalHeaders`](#global-headers)를 재정의합니다.<li>헤더를 제거하려면 값을 빈 문자열로 설정합니다.</ul> |
| `statusCode`   | 아니요       | 리디렉션의 경우 `200`, `301` 또는 `302`입니다. | 응답의 [HTTP 상태 코드](https://developer.mozilla.org/docs/Web/HTTP/Status)입니다. |
| `methods` | 아니요 | 모든 방법 | 경로와 일치하는 요청 메서드 목록입니다. 사용할 수 있는 메서드는 `GET`, `HEAD`, `POST`, `PUT`, `DELETE`, `CONNECT`, `OPTIONS`, `TRACE` 및 `PATCH`입니다. |

각 속성은 요청/응답 파이프라인에서 특정 목적을 갖고 있습니다.

| 용도 | 속성 |
|---|---|
| 경로 일치 | `route`, `methods` |
| 경로가 일치한 후 권한 부여 | `allowedRoles` |
| 규칙이 일치하고 권한이 부여된 후 처리 | `rewrite`(요청 수정) <br><br>`redirect`, `headers`, `statusCode`(응답 수정) |

## <a name="securing-routes-with-roles"></a>역할을 사용하여 경로 보호

하나 이상의 역할 이름을 규칙의 `allowedRoles` 배열에 추가하여 경로를 보호하고, 사용자는 [초대](./authentication-authorization.md)를 통해 사용자 지정 역할에 연결됩니다. 사용 예제는 [예제 구성 파일](#example-configuration-file)을 참조하세요.

기본적으로 모든 사용자는 기본 제공 `anonymous` 역할에 속하며 로그인된 모든 사용자는 `authenticated` 역할의 멤버입니다.

예를 들어 인증된 사용자로만 경로를 제한하려면 기본 제공 `authenticated` 역할을 `allowedRoles` 배열에 추가합니다.

```json
{
  "route": "/profile",
  "allowedRoles": ["authenticated"]
}
```

`allowedRoles` 배열에서 필요에 따라 새 역할을 만들 수 있습니다. 경로를 관리자로만 제한하려면 `allowedRoles` 배열에서 `administrator`라는 고유의 역할을 정의하면 됩니다.

```json
{
  "route": "/admin",
  "allowedRoles": ["administrator"]
}
```

- 역할 이름을 완전히 제어할 수 있습니다. 역할이 준수해야 하는 목록은 없습니다.
- 개별 사용자는 [초대](authentication-authorization.md)를 통해 역할에 연결됩니다.

## <a name="wildcards"></a>와일드카드

와일드 카드 규칙은 경로 패턴의 모든 요청을 매칭하고, 경로 끝에서만 지원되며, 파일 확장명으로 필터링할 수 있습니다. 사용 예제는 [예제 구성 파일](#example-configuration-file)을 참조하세요.

예를 들어 일정 애플리케이션의 경로를 구현하려면 _일정_ 경로에 속하는 모든 URL이 단일 파일을 처리하도록 재작성하면 됩니다.

```json
{
  "route": "/calendar/*",
  "rewrite": "/calendar.html"
}
```

그런 다음, _calendar.html_ 파일은 클라이언트 쪽 라우팅을 사용하여 `/calendar/january/1`, `/calendar/2020` 및 `/calendar/overview`와 같은 URL 변형에 대해 다른 보기를 제공할 수 있습니다.

와일드 카드 일치 항목을 파일 확장명으로 필터링할 수 있습니다. 예를 들어 지정된 경로의 HTML 파일만 매칭하는 규칙을 추가하려는 경우 다음과 같은 규칙을 만들면 됩니다.

```json
{
  "route": "/articles/*.html",
  "headers" : {
    "Cache-Control": "public, max-age=604800, immutable"
  }
}
```

여러 파일 확장명을 필터링하려면 다음 예제와 같이 중괄호 안에 옵션을 포함합니다.

```json
{
  "route": "/images/thumbnails/*.{png,jpg,gif}",
  "headers": {
    "Cache-Control": "public, max-age=604800, immutable"
  }
}
```

와일드 카드 경로의 일반적인 사용 사례는 다음과 같습니다.

- 전체 경로 패턴에 대한 특정 파일 제공
- 다른 HTTP 메서드를 전체 경로 패턴에 매핑
- 인증 및 권한 부여 규칙 적용
- 특수 캐싱 규칙 구현

## <a name="fallback-routes"></a>대체 경로

단일 페이지 애플리케이션은 종종 클라이언트 쪽 라우팅을 사용합니다. 이러한 클라이언트 쪽 라우팅 규칙은 서버에 다시 요청하지 않고 브라우저의 창 위치를 업데이트합니다. 페이지를 새로 고치거나 클라이언트 쪽 회람 규칙에 의해 생성된 URL로 직접 이동하는 경우 적절한 HTML 페이지(일반적으로 클라이언트 쪽 앱의 _index.html_)를 제공하기 위해 서버 쪽 대체 경로가 필요합니다.

다음 예제와 같이 파일 필터를 통해 경로 와일드 카드를 사용하는 대체 경로를 구현하는 규칙을 사용하도록 앱을 구성할 수 있습니다.

```json
{
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": ["/images/*.{png,jpg,gif}", "/css/*"]
  }
}
```

아래의 예제 파일 구조에서 이 규칙을 사용하면 다음과 같은 결과를 얻을 수 있습니다.

```files
├── images
│   ├── logo.png
│   ├── headshot.jpg
│   └── screenshot.gif
│
├── css
│   └── global.css
│
└── index.html
```

| 다음에 대한 요청... | 반환 항목 | 상태 |
| --- | --- | --- |
| */about/* | */index.html* 파일 | `200` |
| */images/logo.png* | 이미지 파일  | `200` |
| */images/icon.svg* | */index.html* 파일 - *svg* 파일 확장명이 `/images/*.{png,jpg,gif}` 필터에 없기 때문   | `200` |
| */images/unknown.png* | 파일 없음 오류  | `404` |
| */css/unknown.css* | 파일 없음 오류  | `404` |
| */css/global.css* | 스타일 시트 파일 | `200` |
| */images* 또는 */css* 폴더 외부에 있는 그 외의 모든 파일 | */index.html* 파일 | `200` |

## <a name="global-headers"></a>글로벌 헤더

`globalHeaders` 섹션에서는 [경로 헤더](#route-headers) 규칙에 의해 재정의되지 않는 한 각 응답에 적용되는 [HTTP 헤더](https://developer.mozilla.org/docs/Web/HTTP/Headers) 세트를 제공합니다. 그렇지 않으면 경로의 헤더와 글로벌 헤더의 합집합이 반환됩니다.

사용 예제는 [예제 구성 파일](#example-configuration-file)을 참조하세요.

헤더를 제거하려면 값을 빈 문자열(`""`)로 설정합니다.

다음은 글로벌 헤더의 일반적인 사용 사례입니다.

- 사용자 지정 캐싱 규칙
- 보안 정책 적용
- 인코딩 설정

## <a name="response-overrides"></a>응답 재정의

`responseOverrides` 섹션에서는 서버가 오류 코드를 반환할 때 사용자 지정 응답을 정의할 수 있는 기회를 제공합니다. 사용 예제는 [예제 구성 파일](#example-configuration-file)을 참조하세요.

다음 HTTP 코드를 재정의할 수 있습니다.

| 상태 코드 | 의미 | 가능한 원인 |
| --- | --- | --- |
| [400](https://developer.mozilla.org/docs/Web/HTTP/Status/400) | 잘못된 요청 | 잘못된 초대 링크 |
| [401](https://developer.mozilla.org/docs/Web/HTTP/Status/401) | 권한 없음 | 인증되지 않은 상태에서 제한된 페이지를 요청 |
| [403](https://developer.mozilla.org/docs/Web/HTTP/Status/403) | 사용할 수 없음 |<ul><li>사용자가 로그인했지만 페이지를 보는 데 필요한 역할이 없습니다.<li>사용자가 로그인했지만 런타임이 ID 클레임에서 사용자 세부 정보를 가져올 수 없습니다.<li>사용자 지정 역할로 사이트에 로그인한 사용자가 너무 많기 때문에 런타임에서 사용자를 로그인 할 수 없습니다.</ul> |
| [404](https://developer.mozilla.org/docs/Web/HTTP/Status/404) | 찾을 수 없음 | 파일을 찾을 수 없습니다. |

다음 예제 구성에서는 오류 코드를 재정의하는 방법을 보여줍니다.

```json
{
    "responseOverrides": {
        "400" : {
            "rewrite": "/invalid-invitation-error.html",
            "statusCode": 200
        },
        "401": {
            "statusCode": 302,
            "redirect": "/login"
        },
        "403": {
            "rewrite": "/custom-forbidden-page.html",
            "statusCode": 200
        },
        "404": {
            "rewrite": "/custom-404.html",
            "statusCode": 200
        }
    }
}
```

## <a name="example-configuration-file"></a>예제 구성 파일

```json
{
    "routes": [
        {
            "route": "/profile",
            "allowedRoles": ["authenticated"]
        },
        {
            "route": "/admin/*",
            "allowedRoles": ["administrator"]
        },
        {
            "route": "/images/*",
            "headers": {
                "cache-control": "must-revalidate, max-age=15770000"
            }
        },
        {
            "route": "/api/*",
            "methods": [ "GET" ],
            "allowedRoles": ["registeredusers"]
        },
        {
            "route": "/api/*",
            "methods": [ "PUT", "POST", "PATCH", "DELETE" ],
            "allowedRoles": ["administrator"]
        },
        {
            "route": "/api/*",
            "allowedRoles": ["authenticated"]
        },
        {
            "route": "/customers/contoso",
            "allowedRoles": ["administrator", "customers_contoso"]
        },
        {
            "route": "/login",
            "rewrite": "/.auth/login/github"
        },
        {
            "route": "/.auth/login/twitter",
            "statusCode": 404,
        },
        {
            "route": "/logout",
            "redirect": "/.auth/logout"
        },
        {
            "route": "/calendar/*",
            "rewrite": "/calendar.html"
        },
        {
            "route": "/specials",
            "redirect": "/deals",
            "statusCode": 301
        }
    ],
    "navigationFallback": {
      "rewrite": "index.html",
      "exclude": ["/images/*.{png,jpg,gif}", "/css/*"]
    },
    "responseOverrides": {
        "400" : {
            "rewrite": "/invalid-invitation-error.html"
        },
        "401": {
            "redirect": "/login",
            "statusCode": 302
        },
        "403": {
            "rewrite": "/custom-forbidden-page.html"
        },
        "404": {
            "rewrite": "/404.html"
        }
    },
    "globalHeaders": {
        "content-security-policy": "default-src https: 'unsafe-eval' 'unsafe-inline'; object-src 'none'"
    },
    "mimeTypes": {
        ".json": "text/json"
    },
}
```

위의 구성에 따라 다음 시나리오를 검토합니다.

| 다음에 대한 요청... | 결과 |
| --- | --- |
| _/profile_ | 인증된 사용자에게는 _/profile/index.html_ 파일이 제공됩니다. 인증되지 않은 사용자는 _/login_ 으로 리디렉션됩니다. |
| _/admin/_ | _관리자_ 역할의 인증된 사용자에게는 _/admin/index.html_ 파일이 제공됩니다. 인증되었지만 _관리자_ 역할에 없는 사용자에게는 `403` 오류<sup>1</sup>이 표시됩니다. 인증되지 않은 사용자는 _/login_ 으로 리디렉션됩니다. |
| _/logo.png_ | 최대 사용 기간이 182일(15,770,000초)을 약간 초과하는 사용자 지정 캐시 규칙을 이미지에 적용합니다. |
| _/api/admin_ | _registeredusers_ 역할이 있는 인증된 사용자의 `GET` 요청은 API로 전송됩니다. 인증되었지만 _registeredusers_ 역할에 없는 사용자와 인증되지 않은 사용자에게는 `401` 오류가 표시됩니다.<br/><br/>_관리자_ 역할의 인증된 사용자가 수행하는 `POST`, `PUT`, `PATCH` 및 `DELETE` 요청은 API로 전송됩니다. 인증되었지만 _관리자_ 역할에 없는 사용자와 인증되지 않은 사용자에게는 `401` 오류가 표시됩니다. |
| _/customers/contoso_ | _관리자_ 또는 _고객\_contoso_ 역할에 속하는 인증된 사용자에게는 _/customers/contoso/index.html_ 파일이 제공됩니다. 인증되었지만 _관리자_ 또는 _고객\_contoso_ 역할에 없는 사용자에게는 `403` 오류<sup>1</sup>가 표시됩니다. 인증되지 않은 사용자는 _/login_ 으로 리디렉션됩니다. |
| _/login_ | 인증되지 않은 사용자는 GitHub를 사용하여 인증해야 합니다. |
| _/.auth/login/twitter_ | 경로 규칙에 따라 Twitter를 통한 권한 부여가 사용되지 않으므로 `404` 오류가 반환되고, _/index.html_ 파일과 `200` 상태 코드를 제공하도록 대체됩니다. |
| _/logout_ | 사용자는 모든 인증 공급자에서 로그아웃됩니다. |
| _/calendar/2021/01_ | 브라우저에는 _/calendar.html_ 파일이 제공됩니다. |
| _/specials_ | 브라우저가 영구적으로 _/deals_ 파일로 리디렉션됩니다. |
| _/data.json_ | `text/json` MIME 형식의 파일이 제공됩니다. |
| _/about_ 또는 클라이언트 쪽 라우팅 패턴과 일치하는 모든 폴더 | _/index.html_ 파일이 `200` 상태 코드와 함께 제공됩니다. |
| _/images/_ 폴더에 없는 파일 | `404` 오류가 표시됩니다. |

<sup>1</sup> [응답 재정의 규칙](#response-overrides)을 사용하여 사용자 지정 오류 페이지를 제공할 수 있습니다.

## <a name="restrictions"></a>제한

_staticwebapps.config.json_ 파일에는 다음과 같은 제한이 있습니다.

- 최대 파일 크기는 100KB
- 고유 역할은 최대 50개

일반적인 제한 사항은 [할당량 문서](quotas.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [인증 및 권한 부여 설정](authentication-authorization.md)

---
author: msmimart
ms.service: active-directory-b2c
ms.subservice: B2C
ms.topic: include
ms.date: 10/16/2019
ms.author: mimart
ms.openlocfilehash: f8d8ffe8c1802a5cf67b7dc2b0fb071b572d76e8
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "95994363"
---
Azure AD B2C 테넌트에 애플리케이션을 등록하려면 새로운 통합 **앱 등록** 환경 또는 레거시 **애플리케이션(레거시)** 환경을 사용하면 됩니다. [새 환경에 대해 자세히 알아보세요](../articles/active-directory-b2c/app-registrations-training-guide.md).

#### <a name="app-registrations"></a>[앱 등록](#tab/app-reg-ga/)

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.
1. 상단 메뉴에서 **디렉터리 + 구독** 필터를 선택한 다음, Azure AD B2C 테넌트가 포함된 디렉터리를 선택합니다.
1. 왼쪽 메뉴에서 **Azure AD B2C** 를 선택합니다. 또는 **모든 서비스** 를 선택하고 **Azure AD B2C** 를 검색하여 선택합니다.
1. **앱 등록** 을 선택한 다음, **새 등록** 을 선택합니다.
1. 애플리케이션의 **이름** 을 입력합니다. 예를 들면 *ROPC_Auth_app* 과 같습니다.
1. 다른 값은 그대로 둔 다음, **등록** 을 선택합니다.
1. 이후 단계에서 사용할 수 있게 **애플리케이션(클라이언트) ID** 를 기록합니다.
1. **관리** 에서 **인증** 을 선택합니다.
1. **새 환경을 체험해 보세요.** (표시되는 경우)를 선택합니다.
1. **기본 클라이언트 유형** 에서 **예** 를 선택하여 애플리케이션을 퍼블릭 클라이언트로 처리합니다. 이 설정은 ROPC 흐름에 필요합니다.
1. **저장** 을 선택합니다.
1. 왼쪽 메뉴에서 **매니페스트** 를 선택하여 매니페스트 편집기를 엽니다. 
1. **oauth2AllowImplicitFlow** 특성을 *true* 로 설정합니다.
    ```json
    "oauth2AllowImplicitFlow": true,
    ```
1. **저장** 을 선택합니다.

#### <a name="applications-legacy"></a>[애플리케이션(레거시)](#tab/applications-legacy/)

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.
1. 상단 메뉴에서 **디렉터리 + 구독** 필터를 선택한 다음, Azure AD B2C 테넌트가 포함된 디렉터리를 선택합니다.
1. 왼쪽 메뉴에서 **Azure AD B2C** 를 선택합니다. 또는 **모든 서비스** 를 선택하고 **Azure AD B2C** 를 검색하여 선택합니다.
1. **애플리케이션(레거시)** 을 선택한 다음, **추가** 를 선택합니다.
1. 애플리케이션의 이름을 입력합니다. 예를 들면 *ROPC_Auth_app* 과 같습니다.
1. **원시 클라이언트** 에 대해 **예** 를 선택합니다.
1. 다른 값은 그대로 둔 다음, **만들기** 를 선택합니다.
1. 이후 단계에서 사용할 **애플리케이션 ID** 를 기록합니다.
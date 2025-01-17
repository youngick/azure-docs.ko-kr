---
title: '자습서: Everbridge와 Azure Active Directory 통합 | Microsoft 문서'
description: Azure Active Directory 및 Everbridge 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 01/27/2021
ms.author: jeedes
ms.openlocfilehash: 6e281931eb4646e09bb9aa3226ed7d0735c84e3f
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "101643782"
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a>자습서: Everbridge와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Everbridge를 통합하는 방법에 대해 알아봅니다.
Azure AD와 Everbridge를 통합하는 경우 다음을 수행할 수 있습니다.

* Everbridge에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 자신의 Azure AD 계정으로 Everbridge에 자동으로 로그인할 수 있도록 합니다. 이 액세스 제어를 SSO(Single Sign-On)라고 합니다.
* Azure Portal을 사용하여 중앙의 한 위치에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

Everbridge와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Single Sign-On을 사용하는 Everbridge 구독입니다.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* Everbridge는 IDP 시작 SSO를 지원합니다.

## <a name="add-everbridge-from-the-gallery"></a>갤러리에서 Everbridge 추가

Everbridge의 Azure AD 통합을 구성하려면 갤러리의 Everbridge를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Everbridge** 를 입력합니다.
1. 결과 패널에서 **Everbridge** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-everbridge"></a>Everbridge에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Everbridge에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Everbridge의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Everbridge에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Everbridge SSO 구성](#configure-everbridge-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Everbridge 테스트 사용자 만들기](#create-everbridge-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Everbridge에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Everbridge** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

    >[!NOTE]
    >애플리케이션을 Azure Portal 및 Everbridge 포털 둘 다에서 관리자 포털 또는  멤버 포털로 구성합니다.

4. **Everbridge** 애플리케이션을 **Everbridge 관리자 포털** 로 구성하려면 **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    ![Everbridge 도메인 및 URL Single Sign-On 정보](common/idp-intiated.png)

    a. **식별자** 상자에 패턴을 따르는 URL을 입력합니다.
    `https://sso.everbridge.net/<API_Name>`

    b. **회신 URL** 상자에 패턴을 따르는 URL을 입력합니다.
    `https://manager.everbridge.net/saml/SSO/<API_Name>/alias/defaultAlias`

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자 및 회신 URL 값으로 이러한 값을 업데이트합니다. 이러한 값을 얻으려면 [Everbridge 지원 팀](mailto:support@everbridge.com)에 문의합니다. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

5. **Everbridge** 애플리케이션을 **Everbridge 멤버 포털** 로 구성하려면 **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

  * IDP 시작 모드로 애플리케이션을 구성하려는 경우 다음 단계를 수행합니다.

     ![IDP 시작 모드에 대한 EverBridge 도메인 및 URL Single Sign-On 정보](common/idp-intiated.png)

    a. **식별자** 상자에 `https://sso.everbridge.net/<API_Name>/<Organization_ID>` 패턴을 따르는 URL을 입력합니다.

    b. **회신 URL** 상자에 `https://member.everbridge.net/saml/SSO/<API_Name>/<Organization_ID>/alias/defaultAlias` 패턴을 따르는 URL을 입력합니다.

   * SP 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 을 선택하고, 다음 단계를 수행합니다.

     ![SP 시작 모드에 대한 Everbridge 도메인 및 URL Single Sign-On 정보](common/both-signonurl.png)

     a. **로그온 URL** 상자에 `https://member.everbridge.net/saml/login/<API_Name>/<Organization_ID>/alias/defaultAlias?disco=true` 패턴을 따르는 URL을 입력합니다.

     > [!NOTE]
     > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL 및 로그온 URL 값을 사용하여 이러한 값을 업데이트합니다. 이러한 값을 얻으려면 [Everbridge 지원 팀](mailto:support@everbridge.com)에 문의합니다. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

6. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 선택하여 **페더레이션 메타데이터 XML** 을 다운로드합니다. 인증서를 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

7. **Everbridge 설정** 섹션에서 요구 사항에 따라 필요한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기 

이 섹션에서는 Azure Portal에서 B.Simon이라는 테스트 사용자를 만듭니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory**, **사용자**, **모든 사용자** 를 차례로 선택합니다.
1. 화면 위쪽에서 **새 사용자** 를 선택합니다.
1. **사용자** 속성에서 다음 단계를 수행합니다.
   1. **이름** 필드에 `B.Simon`을 입력합니다.  
   1. **사용자 이름** 필드에서 username@companydomain.extension을 입력합니다. 예들 들어 `B.Simon@contoso.com`입니다.
   1. **암호 표시** 확인란을 선택한 다음, **암호** 상자에 표시된 값을 적어둡니다.
   1. **만들기** 를 클릭합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Everbridge 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Everbridge** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="configure-everbridge-sso"></a>Everbridge SSO 구성

**Everbridge** 의 SSO를 **Everbridge 관리자 포털** 로 구성하려면 다음 단계를 수행합니다.
 
1. 다른 웹 브라우저 창에서 Everbridge에 관리자 권한으로 로그인합니다.

1. 위쪽 메뉴에서 **설정** 탭을 선택합니다. **보안** 에서 **Single Sign-on** 을 선택합니다.
   
     ![Single Sign-On 구성](./media/everbridge-tutorial/sso.png)
   
     a. **이름** 상자에 식별자 공급자의 이름을 입력합니다. 회사 이름을 예로 들 수 있습니다.
   
     b. **API 이름** 상자에 API의 이름을 입력합니다.
   
     다. **파일 선택** 을 선택하여 Azure Portal에서 다운로드한 메타데이터 파일을 업로드합니다.
   
     d. **SAML ID 위치** 에서 **Subject 문의 NameIdentifier 요소에 ID 포함** 을 선택합니다.
   
     e. **ID 공급자 로그인 URL** 상자에 Azure Portal에서 복사한 **로그인 URL** 값을 붙여넣습니다.
   
     f. **서비스 공급자가 시작한 요청 바인딩** 에서 **HTTP 리디렉션** 을 선택합니다.

     g. **저장** 을 선택합니다.

### <a name="configure-everbridge-as-everbridge-member-portal-sso"></a>Everbridge를 Everbridge 멤버 포털 SSO로 구성

**Everbridge** 의 Single Sign-On을 **EverBridge 멤버 포털** 로 구성하려면 다운로드한 **페더레이션 메타데이터 XML** 을 [Everbridge 지원 팀](mailto:support@everbridge.com)에 보냅니다. 이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.

### <a name="create-everbridge-test-user"></a>Everbridge 테스트 사용자 만들기

이 섹션에서는 Everbridge에서 테스트 사용자인 Britta Simon을 만듭니다. Everbridge 플랫폼에서 사용자를 추가하려면 [Everbridge 지원 팀](mailto:support@everbridge.com)에 문의하세요. Single Sign-On을 사용하려면 먼저 사용자를 만들고 Everbridge에서 활성화해야 합니다. 

### <a name="test-sso"></a>SSO 테스트

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

* Azure Portal에서 이 애플리케이션 테스트를 클릭하면 SSO를 설정한 Everbridge에 자동으로 로그인됩니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Everbridge 타일을 클릭하면 SSO를 설정한 Everbridge에 자동으로 로그인되어야 합니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

Everbridge가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 침입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).
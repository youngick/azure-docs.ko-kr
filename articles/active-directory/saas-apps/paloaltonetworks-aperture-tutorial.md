---
title: '자습서: Palo Alto Networks - Aperture와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Palo Alto Networks - Aperture 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 09/10/2020
ms.author: jeedes
ms.openlocfilehash: 7b4c8ab55a9b2afc9c1a215236fa1276a630a5cf
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97963624"
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---aperture"></a>자습서: Palo Alto Networks - Aperture와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Palo Alto Networks - Aperture를 통합하는 방법에 대해 알아봅니다.
Azure AD에 Palo Alto Networks - Aperture를 통합하면 다음과 같은 이점을 얻을 수 있습니다.

* Palo Alto Networks - Aperture에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 해당 Azure AD 계정으로 Palo Alto Networks - Aperture에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

Palo Alto Networks - Aperture와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 구할 수 있습니다.
* Palo Alto Networks - Aperture Single Sign-On이 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* Palo Alto Networks - Aperture는 **SP** 및 **IDP** 시작 SSO를 지원합니다.

## <a name="adding-palo-alto-networks---aperture-from-the-gallery"></a>갤러리에서 Palo Alto Networks - Aperture 추가

Palo Alto Networks - Aperture의 Azure AD 통합을 구성하려면 갤러리의 Palo Alto Networks - Aperture를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Palo Alto Networks - Aperture** 를 입력합니다.
1. 결과 패널에서 **Palo Alto Networks - Aperture** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso"></a>Azure AD SSO 구성 및 테스트

이 섹션에서는 **B.Simon** 이라는 테스트 사용자를 기반으로 Palo Alto Networks - Aperture에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 Palo Alto Networks - Aperture의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Palo Alto Networks - Aperture에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    * **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
    * **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
2. **[Palo Alto Networks - Aperture SSO 구성](#configure-palo-alto-networks---aperture-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    * **[Palo Alto Networks - Aperture 테스트 사용자 만들기](#create-palo-alto-networks---aperture-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Palo Alto Networks - Aperture에 만듭니다.
3. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Palo Alto Networks - Aperture** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

4. **IDP** 시작 모드에서 애플리케이션을 구성하려면 **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    !["식별자" 및 "회신 URL" 텍스트 상자가 강조 표시되고 "저장" 작업이 선택된 "기본 SAML 구성"을 보여주는 스크린샷.](common/idp-intiated.png)

    a. **식별자** 텍스트 상자에서 `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/metadata` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/auth` 패턴을 사용하여 URL을 입력합니다.

5. **SP** 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 를 클릭하고 다음 단계를 수행합니다.

    ![Palo Alto Networks - Aperture 도메인 및 URL Single Sign-On 정보 SP](common/metadata-upload-additional-signon.png)

    **로그인 URL** 텍스트 상자에서 `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/sign_in` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다. 이러한 값을 얻으려면 [Palo Alto Networks - Aperture 클라이언트 지원 팀](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support)에 문의합니다. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

6. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **인증서(Base64)** 를 다운로드한 다음, 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

7. **Palo Alto Networks - Aperture 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Palo Alto Networks - Aperture에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Palo Alto Networks - Aperture** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-palo-alto-networks---aperture-sso"></a>Palo Alto Networks - Aperture SSO 구성

1. 다른 웹 브라우저 창에서 Palo Alto Networks - Aperture에 관리자로 로그인합니다.

2. 최상위 메뉴 모음에서 **설정** 을 클릭합니다.

    ![설정 탭](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_settings.png)

3. **애플리케이션** 섹션으로 이동하고 메뉴 왼쪽에서 **인증** 을 클릭합니다.

    ![인증 탭](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_auth.png)
    
4. **인증** 페이지에서 다음 단계를 수행합니다.
    
    ![인증 탭](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_singlesignon.png)

    a. **Single Sign-On** 필드에서 **Single Sign-On 사용(지원되는 SSP 공급 기업은 Okta, One login)** 을 선택합니다.

    b. **ID 공급 기업 ID** 텍스트 상자에 Azure Portal에서 복사한 **Azure AD 식별자** 값을 붙여넣습니다.

    다. **파일 선택** 을 클릭하여 Azure AD에서 다운로드한 인증서를 **ID 공급자 인증서** 필드로 업로드합니다.

    d. **ID 공급 기업 SSO URL** 텍스트 상자에 Azure Portal에서 복사한 **로그인 URL** 값을 붙여넣습니다.

    e. **Aperture 정보** 섹션에서 IdP 정보를 살펴보고 **Aperture 키** 필드에서 인증서를 다운로드합니다.

    f. **저장** 을 클릭합니다.


### <a name="create-palo-alto-networks---aperture-test-user"></a>Palo Alto Networks - Aperture 테스트 사용자 만들기

이 섹션에서는 Palo Alto Networks - Aperture에서 Britta Simon이라는 사용자를 만듭니다. [Palo Alto Networks - Aperture 클라이언트 지원 팀](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support)과 함께 협업하여 Palo Alto Networks - Aperture 플랫폼에 사용자를 추가합니다. Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

#### <a name="sp-initiated"></a>SP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Palo Alto Networks - Aperture 로그온 URL로 리디렉션됩니다.  

* Palo Alto Networks - Aperture 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

#### <a name="idp-initiated"></a>IDP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭하면 SSO를 설정한 Palo Alto Networks - Aperture에 자동으로 로그인됩니다. 

Microsoft 내 앱을 사용하여 모든 모드에서 애플리케이션을 테스트할 수도 있습니다. 내 앱에서 Palo Alto Networks - Aperture 타일을 클릭할 때 SP 모드로 구성된 경우 로그인 흐름을 시작하기 위해 애플리케이션 로그온 페이지로 리디렉션되고, IDP 모드로 구성된 경우에는 SSO를 설정한 Palo Alto Networks - Aperture에 자동으로 로그인됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.


## <a name="next-steps"></a>다음 단계

Palo Alto Networks - Aperture가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).
---
title: '자습서: Citrix ADC와 Azure Active Directory Single Sign-On 통합(헤더 기반 인증) | Microsoft Docs'
description: 헤더 기반 인증을 사용하여 Azure Active Directory와 Citrix ADC 간에 SSO(Single Sign-On)를 구성하는 방법을 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 12/16/2020
ms.author: jeedes
ms.openlocfilehash: 9cab0597aeb3bc28f391de558240e5d894f5a49c
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99822061"
---
# <a name="tutorial-azure-active-directory-single-sign-on-integration-with-citrix-adc-header-based-authentication"></a>자습서: Citrix ADC와 Azure Active Directory Single Sign-On 통합(헤더 기반 인증)

이 자습서에서는 Azure AD(Azure Active Directory)와 Citrix ADC를 통합하는 방법에 대해 알아봅니다. Azure AD와 Citrix ADC를 통합하면 다음을 수행할 수 있습니다.

* Azure AD에서 Citrix ADC에 액세스할 수 있는 사용자를 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Citrix ADC에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Citrix ADC SSO(Single Sign-On)가 설정된 구독.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다. 이 자습서에 포함된 시나리오는 다음과 같습니다.

* Citrix ADC에 대한 **SP 시작** SSO

* Citrix ADC에 대한 **Just-In-Time** 사용자 프로비저닝

* [Citrix ADC에 대한 헤더 기반 인증](#publish-the-web-server)

* [Citrix ADC에 대한 Kerberos 기반 인증](citrix-netscaler-tutorial.md#publish-the-web-server)

## <a name="add-citrix-adc-from-the-gallery"></a>갤러리에서 Citrix ADC 추가

Azure AD와 Citrix ADC를 통합하려면 먼저 갤러리의 Citrix ADC를 관리형 SaaS 앱 목록에 추가합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.

1. 왼쪽 메뉴에서 **Azure Active Directory** 를 선택합니다.

1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.

1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.

1. **갤러리에서 추가** 섹션의 검색 상자에서 **Citrix ADC** 를 입력합니다.

1. 결과에서 **Citrix ADC** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-citrix-adc"></a>Citrix ADC에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Citrix ADC에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Citrix ADC의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Citrix ADC에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. [Azure AD SSO 구성](#configure-azure-ad-sso) - 사용자가 이 기능을 사용할 수 있도록 설정합니다.

    1. [Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user) - B.Simon을 사용하여 Azure AD SSO를 테스트합니다.

    1. [Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user) - B.Simon이 Azure AD SSO를 사용할 수 있도록 설정합니다.

1. [Citrix ADC SSO 구성](#configure-citrix-adc-sso) - 애플리케이션 쪽에서 SSO 설정을 구성합니다.

    * [Citrix ADC 테스트 사용자 만들기](#create-a-citrix-adc-test-user) - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Citrix ADC에 만듭니다.

1. [SSO 테스트](#test-sso) - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal을 사용하여 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal에 있는 **Citrix ADC** 애플리케이션 통합 창의 **관리** 아래에서 **Single Sign-On** 을 선택합니다.

1. **Single Sign-On 방법 선택** 창에서 **SAML** 을 선택합니다.

1. **SAML로 Single Sign-On 설정** 창에서 **기본 SAML 구성** 에 대한 펜 모양 **편집** 아이콘을 선택하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 애플리케이션을 **IDP 시작** 모드로 구성합니다.

    1. **식별자** 텍스트 상자에서 `https://<Your FQDN>` 패턴의 URL을 입력합니다.

    1. **회신 URL** 텍스트 상자에 `https://<Your FQDN>/CitrixAuthService/AuthService.asmx` 패턴의 URL을 입력합니다.

1. **SP 시작** 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 을 선택하고, 다음 단계를 수행합니다.

    * **로그온 URL** 텍스트 상자에서 `https://<Your FQDN>/CitrixAuthService/AuthService.asmx` 패턴의 URL을 입력합니다.

    > [!NOTE]
    > * 이 섹션에서 사용되는 URL은 실제 값이 아닙니다. 이러한 값을 식별자, 회신 URL 및 로그온 URL에 대한 실제 값으로 업데이트합니다. 이러한 값을 가져오려면 [Citrix ADC 클라이언트 지원 팀](https://www.citrix.com/contact/technical-support.html)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.
    > * SSO를 설정하려면 공용 웹 사이트에서 URL에 액세스할 수 있어야 합니다. Azure AD에서 토큰을 구성된 URL에 게시할 수 있도록 하려면 Citrix ADC 쪽에서 방화벽 또는 다른 보안 설정을 사용하도록 설정해야 합니다.

1. **SAML로 Single Sign-On 설정** 창의 **SAML 서명 인증서** 섹션에서 **앱 페더레이션 메타데이터 URL** 에 대한 URL을 복사하여 메모장에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

1. Citrix ADC 애플리케이션에는 특정 형식의 SAML 어설션이 필요하므로 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다. 다음 스크린샷에서는 기본 특성의 목록을 보여 줍니다. **편집** 아이콘을 선택하고 특성 매핑을 변경합니다.

    ![SAML 특성 매핑 편집](common/edit-attribute.png)

1. Citrix ADC 애플리케이션에는 SAML 응답에서 다시 전달되는 몇 가지 특성도 추가로 필요합니다. **사용자 특성** 대화 상자의 **사용자 클레임** 아래에서 다음 단계를 수행하여 아래 표와 같은 SAML 토큰 특성을 추가합니다.

    | 속성 | 원본 특성|
    | ---------------| --------------- |
    | mySecretID  | user.userprincipalname |
    
    1. **새 클레임 추가** 를 선택하여 **사용자 클레임 관리** 대화 상자를 엽니다.

    1. **이름** 상자에서 해당 행에 대해 표시된 특성 이름을 입력합니다.

    1. **네임스페이스** 를 비워 둡니다.

    1. **특성** 에 대해 **원본** 을 선택합니다.

    1. **원본 특성** 목록에서 해당 행에 표시된 특성 값을 입력합니다.

    1. **확인** 을 선택합니다.

    1. **저장** 을 선택합니다.

1. **Citrix ADC 설정** 섹션에서 요구 사항에 따라 관련 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션에서는 Azure Portal에서 B.Simon이라는 테스트 사용자를 만듭니다.

1. Azure Portal의 왼쪽 메뉴에서 **Azure Active Directory**, **사용자**, **모든 사용자** 를 차례로 선택합니다.

1. 창 위쪽에서 **새 사용자** 를 선택합니다.

1. **사용자** 속성에서 다음 단계를 완료합니다.

   1. **이름** 에 `B.Simon`를 입력합니다.  

   1. **사용자 이름** 에 대해 _username@companydomain.extension_ 을 입력합니다. `B.Simon@contoso.com`)을 입력합니다.

   1. **암호 표시** 확인란을 선택한 다음, **암호** 에 표시된 값을 적어두거나 복사합니다.

   1. **만들기** 를 선택합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 B.Simon에게 Citrix ADC에 대한 액세스 권한을 부여하여 해당 사용자가 Azure SSO를 사용하도록 설정합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.

1. 애플리케이션 목록에서 **Citrix ADC** 를 선택합니다.

1. 앱 개요의 **관리** 아래에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 **사용자** 목록에서 **B.Simon** 을 선택합니다. **선택** 을 선택합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 을 선택합니다.

## <a name="configure-citrix-adc-sso"></a>Citrix ADC SSO 구성

구성하려는 인증 종류에 대한 단계 링크를 선택합니다.

- [헤더 기반 인증을 위한 Citrix ADC SSO 구성](#publish-the-web-server)

- [Kerberos 기반 인증을 위한 Citrix ADC SSO 구성](citrix-netscaler-tutorial.md#publish-the-web-server)

### <a name="publish-the-web-server"></a>웹 서버 게시 

가상 서버를 만들려면 다음을 수행합니다.

1. **트래픽 관리** > **부하 분산** > **서비스** 를 차례로 선택합니다.
    
1. **추가** 를 선택합니다.

    ![Citrix ADC 구성 - Services 창](./media/header-citrix-netscaler-tutorial/web01.png)

1. 애플리케이션을 실행하는 웹 서버에 대해 다음 값을 설정합니다.

   * **서비스 이름**
   * **서버 IP/기존 서버**
   * **프로토콜**
   * **포트**

     ![Citrix ADC 구성 창](./media/header-citrix-netscaler-tutorial/web01.png)

### <a name="configure-the-load-balancer"></a>부하 분산 장치 구성

부하 분산 장치를 구성하려면 다음을 수행합니다.

1. **트래픽 관리** > **부하 분산** > **가상 서버** 로 차례로 이동합니다.

1. **추가** 를 선택합니다.

1. 다음 스크린샷에서 설명한 대로 다음 값을 설정합니다.

    * **이름**
    * **프로토콜**
    * **IP 주소**
    * **포트**

1. **확인** 을 선택합니다.

    ![Citrix ADC 구성 - Basic Settings 창](./media/header-citrix-netscaler-tutorial/load01.png)

### <a name="bind-the-virtual-server"></a>가상 서버 바인딩

부하 분산 장치를 가상 서버에 바인딩하려면 다음을 수행합니다.

1. **Services and Service Groups(서비스 및 서비스 그룹)** 창에서 **No Load Balancing Virtual Server Service Binding(부하 분산 가상 서버 서비스 바인딩 없음)** 을 선택합니다.

   ![Citrix ADC 구성 - Load Balancing Virtual Server Service Binding 창](./media/header-citrix-netscaler-tutorial/bind01.png)

1. 다음 스크린샷과 같이 설정을 확인한 다음, **닫기** 를 선택합니다.

   ![Citrix ADC 구성 - 가상 서버 서비스 바인딩 확인](./media/header-citrix-netscaler-tutorial/bind02.png)

### <a name="bind-the-certificate"></a>인증서 바인딩

이 서비스를 TLS로 게시하려면 서버 인증서를 바인딩한 다음, 애플리케이션을 테스트합니다.

1. **인증서** 아래에서 **서버 인증서 없음** 을 선택합니다.

   ![Citrix ADC 구성 - 서버 인증서 창](./media/header-citrix-netscaler-tutorial/bind03.png)

1. 다음 스크린샷과 같이 설정을 확인한 다음, **닫기** 를 선택합니다.

   ![Citrix ADC 구성 - 인증서 확인](./media/header-citrix-netscaler-tutorial/bind04.png)

## <a name="citrix-adc-saml-profile"></a>Citrix ADC SAML 프로필

Citrix ADC SAML 프로필을 구성하려면 다음 섹션을 완료합니다.

### <a name="create-an-authentication-policy"></a>인증 정책 만들기

인증 정책을 만들려면 다음을 수행합니다.

1. **Security(보안)**  > **AAA – Application Traffic(애플리케이션 트래픽)**  > **Policies(정책)**  > **Authentication(인증)**  > **Authentication Policies(인증 정책)** 로 차례로 이동합니다.

1. **추가** 를 선택합니다.

1. **인증 정책 만들기** 창에서 다음 값을 입력하거나 선택합니다.

    * **Name**: 인증 정책의 이름을 입력합니다.
    * **작업**: **SAML** 을 입력한 다음, **추가** 를 선택합니다.
    * **식**:  **true** 를 입력합니다.     
    
    ![Citrix ADC 구성 - 인증서 정책 만들기 창](./media/header-citrix-netscaler-tutorial/policy01.png)

1. **만들기** 를 선택합니다.

### <a name="create-an-authentication-saml-server"></a>인증 SAML 서버 만들기

인증 SAML 서버를 만들려면 **인증 SAML 서버 만들기** 창으로 이동한 다음, 다음 단계를 완료합니다.

1. **이름** 에 인증 SAML 서버에 사용할 이름을 입력합니다.

1. **SAML 메타데이터 내보내기** 아래에서 다음을 수행합니다.

   1. **메타데이터 가져오기** 확인란을 선택합니다.

   1. Azure SAML UI에서 이전에 복사한 페더레이션 메타데이터 URL을 입력합니다.
    
1. **발급자 이름** 에 대해 관련 URL을 입력합니다.

1. **만들기** 를 선택합니다.

![Citrix ADC 구성 - 인증 SAML Server 만들기 창](./media/header-citrix-netscaler-tutorial/server01.png)

### <a name="create-an-authentication-virtual-server"></a>인증 가상 서버 만들기

인증 가상 서버를 만들려면 다음을 수행합니다.

1.  **보안** > **AAA – 애플리케이션 트래픽** > **정책** > **인증** > **인증 가상 서버** 로 이동합니다.

1.  **추가** 를 선택한 다음, 다음 단계를 완료합니다.

    1. **이름** 에 인증 가상 서버에 사용할 이름을 입력합니다.

    1. **주소 지정 안 함** 확인란을 선택합니다.

    1. **프로토콜** 에 대해 **SSL** 을 선택합니다.

    1. **확인** 을 선택합니다.

    ![Citrix ADC 구성 - 인증 Virtual Server 창](./media/header-citrix-netscaler-tutorial/server02.png)
    
### <a name="configure-the-authentication-virtual-server-to-use-azure-ad"></a>Azure AD를 사용하도록 인증 가상 서버 구성

인증 가상 서버에 대한 두 개의 섹션을 수정합니다.

1.  **고급 인증 정책** 창에서 **인증 정책 없음** 을 선택합니다.

    ![Citrix ADC 구성 - 고급 인증 정책 창](./media/header-citrix-netscaler-tutorial/virtual01.png)

1. **정책 바인딩** 창에서 인증 정책을 선택한 다음, **바인딩** 를 선택합니다.

    ![Citrix ADC 구성 - Policy Binding 창](./media/header-citrix-netscaler-tutorial/virtual02.png)

1. **양식 기반 가상 서버** 창에서 **부하 분산 가상 서버 없음** 을 선택합니다.

    ![Citrix ADC 구성 - 양식 기반 Virtual Servers 창](./media/header-citrix-netscaler-tutorial/virtual03.png)

1. **인증 FQDN** 에 대해 FQDN(정규화된 도메인 이름)을 입력합니다(필수).

1. Azure AD 인증을 사용하여 보호하려는 부하 분산 가상 서버를 선택합니다.

1. **바인딩** 을 선택합니다.

    ![Citrix ADC 구성 - Load Balancing Virtual Server Binding 창](./media/header-citrix-netscaler-tutorial/virtual04.png)

    > [!NOTE]
    > **인증 가상 서버 구성** 창에서 **완료** 를 선택해야 합니다.

1. 변경 내용을 확인하려면 브라우저에서 애플리케이션 URL로 이동합니다. 이전에 확인한 인증되지 않은 액세스 대신 테넌트 로그인 페이지가 표시됩니다.

    ![Citrix ADC 구성 - 웹 브라우저의 로그인 페이지](./media/header-citrix-netscaler-tutorial/virtual05.png)

## <a name="configure-citrix-adc-sso-for-header-based-authentication"></a>헤더 기반 인증을 위한 Citrix ADC SSO 구성

### <a name="configure-citrix-adc"></a>Citrix ADC 구성

헤더 기반 인증을 위해 Citrix ADC를 구성하려면 다음 섹션을 완료합니다.

#### <a name="create-a-rewrite-action"></a>다시 쓰기 작업 만들기

1. **AppExpert** > **Rewrite(다시 쓰기)**  > **Rewrite Actions(다시 쓰기 작업)** 로 차례로 이동합니다.
 
    ![Citrix ADC 구성 - 재작성 작업 창](./media/header-citrix-netscaler-tutorial/header01.png)

1.  **Add(추가)** 를 선택하고, 다음 단계를 완료합니다.

    1. **Name(이름)** 에 대해 다시 쓰기 작업의 이름을 입력합니다.

    1. **Type(형식)** 에 대해 **INSERT_HTTP_HEADER** 를 입력합니다.

    1. **Header Name(헤더 이름)** 에 대해 헤더 이름을 입력합니다(이 예에서는 _SecretID_ 사용).

    1. **Expression(식)** 에 대해 **aaa.USER.ATTRIBUTE("mySecretID")** 를 입력합니다. 여기서 **mySecretID** 는 Citrix ADC로 보낸 Azure AD SAML 클레임입니다.

    1. **만들기** 를 선택합니다.

    ![Citrix ADC 구성 - 재작성 작업 만들기 창](./media/header-citrix-netscaler-tutorial/header02.png)
 
#### <a name="create-a-rewrite-policy"></a>다시 쓰기 정책 만들기

1.  **AppExpert** > **Rewrite(다시 쓰기)**  > **Rewrite Policies(다시 쓰기 정책)** 로 차례로 이동합니다.
 
    ![Citrix ADC 구성 - 재작성 정책 창](./media/header-citrix-netscaler-tutorial/header03.png)

1.  **Add(추가)** 를 선택하고, 다음 단계를 완료합니다.

    1. **Name(이름)** 에 대해 다시 쓰기 정책의 이름을 입력합니다.

    1. **Action(작업)** 에 대해 이전 섹션에서 만든 다시 쓰기 작업을 선택합니다.

    1. **Expression(식)** 에 대해 **true** 를 입력합니다.

    1. **만들기** 를 선택합니다.

    ![Citrix ADC 구성 - 재작성 정책 만들기 창](./media/header-citrix-netscaler-tutorial/header04.png)

### <a name="bind-a-rewrite-policy-to-a-virtual-server"></a>가상 서버에 다시 쓰기 정책 바인딩

GUI를 사용하여 다시 쓰기 정책을 가상 서버에 바인딩하려면,

1. **트래픽 관리** > **부하 분산** > **가상 서버** 로 차례로 이동합니다.

1. 가상 서버 목록에서 다시 쓰기 정책을 바인딩하려는 가상 서버를 선택한 다음, **열기** 를 선택합니다.

1. **부하 분산 가상 서버** 창의 **고급 설정** 아래에서 **정책** 을 선택합니다. NetScaler 인스턴스에 대해 구성된 모든 정책이 목록에 표시됩니다.
 
    !["이름", "작업" 및 "식" 필드가 강조 표시되고 "만들기" 단추가 선택된 "구성" 탭을 보여주는 스크린샷.](./media/header-citrix-netscaler-tutorial/header05.png)

    ![Citrix ADC 구성 - Load Balancing Virtual Server 창](./media/header-citrix-netscaler-tutorial/header06.png)

1.  이 가상 서버에 바인딩하려는 정책 이름 옆의 확인란을 선택합니다.
 
    ![Citrix ADC 구성 - Load Balancing Virtual Server Traffic Policy Binding 창](./media/header-citrix-netscaler-tutorial/header08.png)

1. **형식 선택** 대화 상자에서

    1. **정책 선택** 에 대해 **트래픽** 을 선택합니다.

    1. **Choose Type(형식 선택)** 에 대해 **Request(요청)** 를 선택합니다.

    ![Citrix ADC 구성 - 정책 대화 상자](./media/header-citrix-netscaler-tutorial/header07.png)

1.  **확인** 을 선택합니다. 상태 표시줄의 메시지에서 정책이 성공적으로 구성되었음을 나타냅니다.

### <a name="modify-the-saml-server-to-extract-attributes-from-a-claim"></a>클레임에서 특성을 추출하도록 SAML 서버 수정

1.  **Security(보안)**  > **AAA – Application Traffic(애플리케이션 트래픽)**  > **Policies(정책)**  > **Authentication(인증)**  > **Advanced Policies(고급 정책)**  > **Actions(작업)**  > **Servers(서버)** 로 차례로 이동합니다.

1.  애플리케이션에 적절한 인증 SAML 서버를 선택합니다.
 
    ![Citrix ADC 구성 - 인증 SAML Server 구성 창](./media/header-citrix-netscaler-tutorial/header09.png)

1. **Attributes(특성)** 창에서 추출하려는 SAML 특성을 쉼표로 구분하여 입력합니다. 이 예에서는 `mySecretID` 특성을 입력합니다.
 
    ![Citrix ADC 구성 - Attributes 창](./media/header-citrix-netscaler-tutorial/header10.png)

1. 액세스를 확인하려면 브라우저의 URL에 있는 **Headers Collection(헤더 컬렉션)** 아래에서 SAML 특성을 찾습니다.

    ![Citrix ADC 구성 - URL에 있는 헤더 컬렉션](./media/header-citrix-netscaler-tutorial/header11.png)

### <a name="create-a-citrix-adc-test-user"></a>Citrix ADC 테스트 사용자 만들기

이 섹션에서는 Citrix ADC에서 B.Simon이라는 사용자를 만듭니다. Citrix ADC는 Just-In-Time 사용자 프로비저닝을 지원하며, 기본적으로 사용하도록 설정되어 있습니다. 이 섹션에서 수행할 작업이 없습니다. Citrix ADC에 사용자가 아직 없는 경우 인증 후에 새 사용자가 만들어집니다.

> [!NOTE]
> 사용자를 수동으로 만들어야 하는 경우 [Citrix ADC 클라이언트 지원 팀](https://www.citrix.com/contact/technical-support.html)에 문의하세요.

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Citrix ADC 로그온 URL로 리디렉션됩니다. 

* Citrix ADC 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Citrix ADC 타일을 클릭하면 Citrix ADC 로그온 URL로 리디렉션됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.


## <a name="next-steps"></a>다음 단계

Citrix ADC가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).
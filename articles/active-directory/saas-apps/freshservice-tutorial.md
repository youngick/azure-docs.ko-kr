---
title: '자습서: Freshservice와 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory 및 Freshservice 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 01/15/2021
ms.author: jeedes
ms.openlocfilehash: fb8b12cdb8fd9ed37ac4086d213183e800d6febc
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "101651761"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-freshservice"></a>자습서: Freshservice와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Freshservice를 통합하는 방법에 대해 알아봅니다. Azure AD와 Freshservice를 통합하면 다음 작업을 할 수 있습니다.

* Freshservice에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Freshservice에 자동으로 로그인되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Freshservice SSO(Single Sign-On)가 가능하도록 설정된 구독

> [!NOTE]
> 이 통합은 Azure AD 미국 정부 클라우드 환경에서도 사용할 수 있습니다. 이 애플리케이션은 Azure AD 미국 정부 클라우드 애플리케이션 갤러리에서 찾을 수 있으며 퍼블릭 클라우드에서와 동일한 방법으로 구성할 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Freshservice에서 **SP** 시작 SSO를 지원합니다.

## <a name="add-freshservice-from-the-gallery"></a>갤러리에서 Freshservice 추가

Freshservice의 Azure AD 통합을 구성하려면 갤러리의 Freshservice를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Freshservice** 를 입력합니다.
1. 결과 패널에서 **Freshservice** 를 선택한 후 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-freshservice"></a>Freshservice에 대한 Azure AD SSO 구성 및 테스트

테스트 사용자 **B.Simon** 을 사용하여 Freshservice로 Azure AD SSO를 구성 및 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Freshservice의 관련 사용자 간에 연결 관계가 설정되어야 합니다.

Freshservice에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Freshservice SSO 구성](#configure-freshservice-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Freshservice 테스트 사용자 만들기](#create-freshservice-test-user)** - Azure AD 표현과 연결된 B.Simon에 해당하는 사용자를 Freshservice에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Freshservice** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 다음 필드에 대한 값을 입력합니다.

    a. **로그인 URL** 텍스트 상자에서 `https://<company-name>.freshservice.com` 패턴을 사용하여 URL을 입력합니다.

    b. **식별자(엔터티 ID)** 텍스트 상자에서 `https://<company-name>.freshservice.com` 패턴을 사용하는 URL을 입력합니다.

    다. **회신 URL** 텍스트 상자에서 `https://<company-name>.freshservice.com/login/saml` 패턴을 사용하여 URL을 입력합니다.
    
    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 이러한 값을 실제 로그온 URL, 식별자 및 회신 URL로 업데이트합니다. 이러한 값을 얻으려면 [Freshservice 클라이언트 지원 팀](https://support.freshservice.com/)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **인증서(Base64)** 를 찾은 후 **다운로드** 를 선택하여 인증서를 컴퓨터에 다운로드하고 본인의 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

1. **Azure Portal** 의 **Freshservice 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Freshservice에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Freshservice** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-freshservice-sso"></a>Freshservice SSO 구성

1. Freshservice 내에서 구성을 자동화하려면 **확장 설치** 를 클릭하여 **내 앱 보안 로그인 브라우저 확장** 을 설치해야 합니다.

    ![내 앱 확장](common/install-myappssecure-extension.png)

1. 브라우저에 확장을 추가한 후 **Freshservice 설정** 을 클릭하면 Freshservice 애플리케이션으로 이동됩니다. 애플리케이션에서 관리자 자격 증명을 입력하여 Freshservice에 로그인합니다. 브라우저 확장이 애플리케이션을 자동으로 구성하고 3-6단계를 자동으로 수행합니다.

    ![설정 구성](common/setup-sso.png)

1. Freshservice를 수동으로 설정하려면 Freshservice 회사 사이트에 관리자 권한으로 로그인합니다.

1. 왼쪽 메뉴에서 **관리자** 를 클릭하고, **일반 설정** 에서 **기술 지원팀 보안** 을 선택합니다.

    ![관리자](./media/freshservice-tutorial/configure-1.png "Admin")

1. **보안** 에서 **Freshservice 360 보안으로 이동** 을 클릭합니다.

    ![보안](./media/freshservice-tutorial/configure-2.png "보안")

1. **보안** 섹션에서 다음 단계를 수행합니다.

    ![Single Sign-On](./media/freshservice-tutorial/configure-3.png "Single Sign On")
  
    a. **Single Sign On** 에서 **켬** 을 선택합니다.

    b. **로그인 방법** 에서 **SAML SSO** 를 선택합니다.

    다. Azure Portal에서 복사한 **엔터티 ID** 값을 **IDP에서 제공한 엔터티 ID** 텍스트 상자에 붙여넣습니다.

    d. **SAML SSO URL** 텍스트 상자에 Azure Portal에서 복사한 **로그인 URL** 값을 붙여넣습니다.

    e. **서명 옵션** 의 드롭다운에서 **서명된 어설션만** 을 선택합니다.

    f. **로그아웃 URL** 텍스트 상자에 Azure Portal에서 복사한 **로그아웃 URL** 값을 붙여넣습니다.

    g. 앞에서 얻은 **인증서(Base64)** 값을 **보안 인증서** 텍스트 상자에 붙여넣습니다.
  
    h. **저장** 을 클릭합니다.


## <a name="create-freshservice-test-user"></a>Freshservice 테스트 사용자 만들기

Azure AD 사용자가 FreshService에 로그인할 수 있도록 하려면 FreshService로 프로비저닝되어야 합니다. FreshService의 경우 프로비전은 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. **FreshService** 회사 사이트에 관리자 권한으로 로그인합니다.

2. 왼쪽 메뉴에서 **관리자** 를 클릭합니다.

3. **사용자 관리** 섹션에서 **요청자** 를 클릭합니다.

    ![요청자](./media/freshservice-tutorial/create-user-1.png "요청자")

4. **새 요청자** 를 클릭합니다.

    ![새 요청자](./media/freshservice-tutorial/create-user-2.png "새 요청자")

5. **새 요청자** 섹션에서 필요한 필드를 입력하고 **저장** 을 클릭합니다.
    ![새 요청자](./media/freshservice-tutorial/create-user-3.png "새 요청자")  

    > [!NOTE]
    > Azure Active Directory 계정 보유자는 활성화되기 전에 계정을 확인하기 위한 링크가 포함된 전자 메일을 받습니다.
    >  

    > [!NOTE]
    > 다른 FreshService 사용자 계정 생성 도구 또는 FreshService가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비저닝할 수 있습니다.

## <a name="test-sso"></a>SSO 테스트

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Freshservice 로그온 URL로 리디렉션됩니다. 

* Freshservice 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Freshservice 타일을 클릭하면 SSO를 설정한 Freshservice에 자동으로 로그인됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

 Freshservice가 구성되면 세션 제어를 적용하여 조직의 중요 데이터에 대한 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).
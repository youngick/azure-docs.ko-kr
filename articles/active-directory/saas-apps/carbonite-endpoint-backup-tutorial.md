---
title: '자습서: Carbonite Endpoint Backup과 Azure Active Directory 연결 | Microsoft Docs'
description: Azure Active Directory와 Carbonite Endpoint Backup 간에 Single Sign-On을 구성하는 방법을 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/06/2019
ms.author: jeedes
ms.openlocfilehash: ff19275270e5b6572fb7d637b88c4736a3aa6ea0
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92456486"
---
# <a name="tutorial-integrate-carbonite-endpoint-backup-with-azure-active-directory"></a>자습서: Azure Active Directory와 Carbonite Endpoint Backup 연결

이 자습서에서는 Azure AD(Azure Active Directory)와 Carbonite Endpoint Backup을 연결하는 방법에 대해 알아봅니다. Azure AD와 Carbonite Endpoint Backup을 연결하면 다음 작업을 수행할 수 있습니다.

* Azure AD에서 Carbonite Endpoint Backup에 액세스할 수 있는 사용자를 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Carbonite Endpoint Backup에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Carbonite Endpoint Backup SSO(Single Sign-On)를 사용하도록 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Carbonite Endpoint Backup에서 **SP 및 IDP** 시작 SSO를 지원합니다.

## <a name="adding-carbonite-endpoint-backup-from-the-gallery"></a>갤러리에서 Carbonite Endpoint Backup 추가

Carbonite Endpoint Backup이 Azure AD에 연결되도록 구성하려면 갤러리에서 Carbonite Endpoint Backup을 관리형 SaaS 앱 목록에 추가해야 합니다.

1. [Azure Portal](https://portal.azure.com)에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Carbonite Endpoint Backup** 을 입력합니다.
1. 결과 패널에서 **Carbonite Endpoint Backup** 을 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Carbonite Endpoint Backup에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Carbonite Endpoint Backup의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Carbonite Endpoint Backup에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Carbonite Endpoint Backup SSO 구성](#configure-carbonite-endpoint-backup-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
3. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
5. **[Carbonite Endpoint Backup 테스트 사용자 만들기](#create-carbonite-endpoint-backup-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Carbonite Endpoint Backup에 만듭니다.
6. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **Carbonite Endpoint Backup** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾고, **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **IDP** 섹션에서 애플리케이션을 구성하려면 **기본 SAML 구성** 섹션에서 다음 필드 값을 입력합니다.

    a. **식별자** 텍스트 상자에서 다음 URL 중 하나를 입력합니다.

    ```http
    https://red-us.mysecuredatavault.com
    https://red-apac.mysecuredatavault.com
    https://red-fr.mysecuredatavault.com
    https://red-emea.mysecuredatavault.com
    https://kamino.mysecuredatavault.com
    ```

    b. **회신 URL** 텍스트 상자에서 다음 URL 중 하나를 입력합니다.

    ```http
    https://red-us.mysecuredatavault.com/AssertionConsumerService.aspx
    https://red-apac.mysecuredatavault.com/AssertionConsumerService.aspx
    https://red-fr.mysecuredatavault.com/AssertionConsumerService.aspx
    https://red-emea.mysecuredatavault.com/AssertionConsumerService.aspx
    ```

1. **SP** 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 를 클릭하고 다음 단계를 수행합니다.

    **로그온 URL** 텍스트 상자에서 다음 URL 중 하나를 입력합니다.

    ```http
    https://red-us.mysecuredatavault.com/
    https://red-apac.mysecuredatavault.com/
    https://red-fr.mysecuredatavault.com/
    https://red-emea.mysecuredatavault.com/
    ```

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **인증서(Base64)** 를 찾은 후 **다운로드** 를 선택하여 인증서를 다운로드하고 본인의 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

1. **Carbonite Endpoint Backup 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

### <a name="configure-carbonite-endpoint-backup-sso"></a>Carbonite Endpoint Backup SSO 구성

1. Carbonite Endpoint Backup 내에서 구성을 자동화하려면 **확장 설치** 를 클릭하여 **내 앱 보안 로그인 브라우저 확장** 을 설치해야 합니다.

    ![내 앱 확장](common/install-myappssecure-extension.png)

2. 브라우저에 확장을 추가한 후 **Carbonite Endpoint Backup 설정** 을 클릭하면 Carbonite Endpoint Backup 애플리케이션으로 안내합니다. 여기서 관리자 자격 증명을 입력하여 Carbonite Endpoint Backup에 로그인합니다. 브라우저 확장에서 애플리케이션을 자동으로 구성하고 3-7단계를 자동화합니다.

    ![설정 구성](common/setup-sso.png)

3. Carbonite Endpoint Backup을 수동으로 설정하려면 새 웹 브라우저 창을 열고 Carbonite Endpoint Backup 회사 사이트에 관리자로 로그인한 후에 다음 단계를 수행합니다.

4. 왼쪽 창에서 **Company**(회사)를 클릭합니다.

    ![스크린샷은 회사에서 선택한 Carbonite 엔드포인트를 보여줍니다.](media/carbonite-endpoint-backup-tutorial/configure1.png)

5. **Single sign-on** 을 클릭합니다.

    ![스크린샷은 Single Sign-On이 선택된 회사를 보여줍니다.](media/carbonite-endpoint-backup-tutorial/configure2.png)

6. **Enable**(사용)을 클릭한 다음, **Edit settings**(설정 편집)를 클릭하여 구성합니다.

    ![스크린샷은 사용 및 편집 설정이 호출된 Single Sign-On 탭을 보여줍니다.](media/carbonite-endpoint-backup-tutorial/configure3.png)

7. **Single sign-on** 설정 페이지에서 다음 단계를 수행합니다.

    ![스크린샷은 이 단계에서 설명한 정보가 포함된 Single Sign-On 탭을 보여줍니다.](media/carbonite-endpoint-backup-tutorial/configure4.png)

    1. Azure Portal에서 복사한 **Azure AD 식별자** 값을 **ID 공급자 이름** 텍스트 상자에 붙여넣습니다.

    1. Azure Portal에서 복사한 **로그인 URL** 값을 **ID 공급자 URL** 텍스트 상자에 붙여넣습니다.

    1. **Choose file**(파일 선택)을 클릭하여 Azure Portal로부터 다운로드한 **인증서(Base64)** 를 업로드합니다.

    1. **저장** 을 클릭합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Carbonite Endpoint Backup에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Carbonite Endpoint Backup** 을 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.

   !["사용자 및 그룹" 링크](common/users-groups-blade.png)

1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![사용자 추가 링크](common/add-assign-user.png)

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. SAML 어설션에 역할 값이 필요한 경우 **역할 선택** 대화 상자의 목록에서 사용자에 대한 적절한 역할을 선택한 다음, 화면의 아래쪽에 있는 **선택** 단추를 클릭합니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="create-carbonite-endpoint-backup-test-user"></a>Carbonite Endpoint Backup 테스트 사용자 만들기

1. 다른 웹 브라우저 창에서 Carbonite Endpoint Backup 회사 사이트에 관리자 권한으로 로그인합니다.

1. 왼쪽 창에서 **Users**(사용자)를 클릭한 다음, **Add user**(사용자 추가)를 클릭합니다.

    ![스크린샷은 사용자와 사용자 추가가 선택된 Carbonite 엔드포인트 페이지를 보여줍니다.](media/carbonite-endpoint-backup-tutorial/adduser1.png)

1. **Add user** 페이지에서 다음 단계를 수행합니다.

    ![스크린샷은 여기에 설명된 단계를 수행할 수 있는 사용자 추가 페이지를 보여줍니다.](media/carbonite-endpoint-backup-tutorial/adduser2.png)

    1. 사용자의 **Email**(이메일), **First name**(이름), **Last name**(성)을 입력하고, 조직의 요구 사항에 따라 사용자에게 필요한 권한을 제공합니다.

    1. **사용자 추가** 를 클릭합니다.

### <a name="test-sso"></a>SSO 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Carbonite Endpoint Backup 타일을 클릭하면 SSO를 설정한 Carbonite Endpoint Backup에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS 앱을 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란?](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)
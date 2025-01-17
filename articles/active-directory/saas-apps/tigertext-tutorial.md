---
title: '자습서: TigerConnect Secure Messenger와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory와 TigerConnect Secure Messenger 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/21/2020
ms.author: jeedes
ms.openlocfilehash: 6831e96ebd8fd2db51d640ff3d93955b1a9f1477
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96182158"
---
# <a name="tutorial-azure-active-directory-integration-with-tigerconnect-secure-messenger"></a>자습서: TigerConnect Secure Messenger와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 TigerConnect Secure Messenger를 통합하는 방법에 대해 알아봅니다.

TigerConnect Secure Messenger를 Azure AD와 통합하면 다음과 같은 이점을 누릴 수 있습니다.

* TigerConnect Secure Messenger에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 자신의 Azure AD 계정으로 TigerConnect Secure Messenger에 자동으로 로그인(Single Sign-On)하도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On](../manage-apps/what-is-single-sign-on.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

TigerConnect Secure Messenger와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.
* Single Sign-On이 설정된 TigerConnect Secure Messenger 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트한 후 Azure AD에 TigerConnect Secure Messenger를 통합합니다.

* TigerConnect Secure Messenger는 **SP** 시작 SSO를 지원합니다.
* TigerConnect Secure Messenger가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-tigerconnect-secure-messenger-from-the-gallery"></a>갤러리에서 TigerConnect Secure Messenger 추가

TigerConnect Secure Messenger의 Azure AD 통합을 구성하려면 갤러리의 TigerConnect Secure Messenger를 관리형 SaaS 앱 목록에 추가해야 합니다.

1. [Azure Portal](https://portal.azure.com)에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **TigerConnect Secure Messenger** 를 입력합니다.
1. 결과 패널에서 **TigerConnect Secure Messenger** 를 선택하고 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso"></a>Azure AD SSO 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 TigerConnect Secure Messenger에서 Azure AD Single Sign-On을 구성하고 테스트합니다. Single Sign-On이 작동하려면 Azure AD 사용자와 TigerConnect Secure Messenger의 관련 사용자 간에 연결을 설정해야 합니다.

TigerConnect Secure Messenger에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. 사용자가 이 기능을 사용할 수 있도록 **[Azure AD SSO를 구성](#configure-azure-ad-sso)** 합니다.
    * **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
    * **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
1. **[TigerConnect Secure Messenger SSO 구성](#configure-tigerconnect-secure-messenger-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    * **[TigerConnect Secure Messenger 테스트 사용자 만들기](#create-a-tigerconnect-secure-messenger-test-user)** - Britta Simon이라는 Azure AD 사용자와 연결된 TigerConnect Secure Messenger의 Britta Simon이라는 사용자가 있습니다.
1. **[SSO를 테스트](#test-sso)** 하여 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정합니다.

TigerConnect Secure Messenger에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **TigerConnect Secure Messenger** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾은 다음, **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 다음 필드에 대한 값을 입력합니다.

    1. **로그온 URL** 상자에 URL을 입력합니다.

       `https://home.tigertext.com`

    1. **식별자(엔터티 ID)** 상자에서 다음 패턴을 사용하여 URL을 입력합니다.

       `https://saml-lb.tigertext.me/v1/organization/<instance ID>`

    > [!NOTE]
    > **식별자(엔터티 ID)** 값은 실제 값이 아닙니다. 실제 식별자로 이 값을 업데이트하세요. 이 값을 얻으려면 [TigerConnect Secure Messenger 고객 지원 팀](mailto:prosupport@tigertext.com)에 문의하세요. Azure Portal의 **기본 SAML 구성** 창에 표시된 패턴을 참조할 수도 있습니다.

1. **SAML로 Single Sign-On 설정** 창의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 선택하여 지정된 옵션에서 **페더레이션 메타데이터 XML** 을 다운로드하고, 컴퓨터에 저장합니다.

    ![페더레이션 메타데이터 XML 다운로드 옵션](common/metadataxml.png)

1. **TigerConnect Secure Messenger 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 TigerConnect Secure Messenger에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **TigerConnect Secure Messenger** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.

   !["사용자 및 그룹" 링크](common/users-groups-blade.png)

1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![사용자 추가 링크](common/add-assign-user.png)

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. SAML 어설션에 역할 값이 필요한 경우 **역할 선택** 대화 상자의 목록에서 사용자에 대한 적절한 역할을 선택한 다음, 화면의 아래쪽에 있는 **선택** 단추를 클릭합니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-tigerconnect-secure-messenger-sso"></a>TigerConnect Secure Messenger SSO 구성

TigerConnect Secure Messenger 쪽에서 Single Sign-On을 구성하려면 Azure Portal에서 다운로드한 페더레이션 메타데이터 XML과 적절히 복사한 URL을 [TigerConnect Secure Messenger 지원 팀](mailto:prosupport@tigertext.com)으로 보내야 합니다. TigerConnect Secure Messenger 팀이 양쪽 모두에서 SAML SSO 연결이 올바르게 설정되어 있는지 확인합니다.

## <a name="create-a-tigerconnect-secure-messenger-test-user"></a>TigerConnect Secure Messenger 테스트 사용자 만들기

이 섹션에서는 TigerConnect Secure Messenger에서 Britta Simon이라는 사용자를 만듭니다. [TigerConnect Secure Messenger 지원 팀](mailto:prosupport@tigertext.com)과 협력하여 Britta Simon을 TigerConnect Secure Messenger의 사용자로 추가하세요. Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.

## <a name="test-sso"></a>SSO 테스트

이 섹션에서는 My Apps 포털을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

내 앱 포털에서 **TigerConnect Secure Messenger** 를 선택하면 SSO를 설정한 TigerConnect Secure Messenger 구독에 자동으로 로그인됩니다. My Apps 포털에 대한 자세한 내용은 [My Apps 포털에서 앱 액세스 및 사용](../user-help/my-apps-portal-end-user-access.md)을 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS 앱 통합에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)

- [Azure AD가 포함된 TigerConnect Secure Messenger 사용해 보기](https://aad.portal.azure.com/)

- [Microsoft Cloud App Security의 세션 제어란?](/cloud-app-security/proxy-intro-aad)
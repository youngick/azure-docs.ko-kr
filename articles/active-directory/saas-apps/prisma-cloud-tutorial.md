---
title: '자습서: Prisma Cloud SSO와 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory와 Prisma Cloud SSO 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/08/2021
ms.author: jeedes
ms.openlocfilehash: d92ca345b0800523d86ce7b42220209a1f237103
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "101651429"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-prisma-cloud-sso"></a>자습서: Prisma Cloud SSO와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Prisma Cloud SSO와 Azure AD(Azure Active Directory)를 통합하는 방법에 대해 알아봅니다. Azure AD와 Prisma Cloud SSO를 통합하는 경우 다음을 수행할 수 있습니다.

* Prisma Cloud SSO에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 자신의 Azure AD 계정으로 Prisma Cloud SSO에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Prisma Cloud SSO SSO(Single Sign-On)가 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Prisma Cloud SSO에서 **IDP** 시작 SSO를 지원합니다.

* Prisma Cloud SSO에서 **Just In Time** 사용자 프로비저닝을 지원합니다.

## <a name="add-prisma-cloud-sso-from-the-gallery"></a>갤러리에서 Prisma Cloud SSO 추가

Prisma Cloud SSO가 Azure AD에 통합되도록 구성하려면 갤러리에서 Prisma Cloud SSO를 관리형 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Prisma Cloud SSO** 를 입력합니다.
1. 결과 패널에서 **Prisma Cloud SSO** 를 선택한 후 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-prisma-cloud-sso"></a>Prisma Cloud SSO에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Prisma Cloud SSO에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Prisma Cloud SSO의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Prisma Cloud SSO에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Prisma Cloud SSO 구성](#configure-prisma-cloud-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Prisma Cloud SSO 테스트 사용자 만들기](#create-prisma-cloud-sso-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Prisma Cloud SSO에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Prisma Cloud SSO** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **SAML로 Single Sign-On 설정** 페이지에서 다음 필드에 값을 입력합니다.

    a. **식별자** 텍스트 상자에서 `https://app2.prismacloud.io/customer/<CUSTOMERID>` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 값은 고정되어 있으며 Azure Portal에 미리 채워져 있습니다. 요구 사항에 따라 적절한 URL을 선택해야 합니다.

    > [!NOTE]
    > 식별자 값은 실제 값이 아닙니다. 실제 식별자로 값을 업데이트하세요. 이 값을 얻으려면 [Prisma Cloud SSO 클라이언트 지원 팀](mailto:support@paloaltonetworks.com)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **인증서(Base64)** 를 찾은 후 **다운로드** 를 선택하여 인증서를 다운로드하고 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

1. **Prisma Cloud SSO 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Prisma Cloud SSO에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Prisma Cloud SSO** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-prisma-cloud-sso"></a>Prisma Cloud 클라우드 SSO 구성

**Prisma Cloud SSO** 쪽에서 Single Sign-On을 구성하려면 Azure Portal에서 다운로드한 **인증서(Base64)** 와 적절히 복사한 URL을 [Prisma Cloud SSO 지원 팀](mailto:support@paloaltonetworks.com)으로 보내야 합니다. 이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.

### <a name="create-prisma-cloud-sso-test-user"></a>Prisma Cloud SSO 테스트 사용자 만들기

이 섹션에서는 Prisma Cloud SSO에서 B.Simon이라는 사용자를 만듭니다. Prisma Cloud SSO는 기본적으로 사용하도록 설정된 Just-In-Time 프로비저닝을 지원합니다. 이 섹션에 작업 항목이 없습니다. Prisma Cloud SSO에 사용자가 아직 없는 경우 Prisma Cloud SSO에 액세스하려고 할 때 새 사용자가 만들어집니다.

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

* Azure Portal에서 이 애플리케이션 테스트를 클릭하면 SSO를 설정한 Prisma Cloud SSO에 자동으로 로그인됩니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Prisma Cloud SSO타일을 클릭하면 SSO를 설정한 Prisma Cloud SSO에 자동으로 로그인됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

Prisma Cloud SSO가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).
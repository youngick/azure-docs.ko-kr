---
title: '자습서: Snowflake와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Snowflake 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 12/27/2020
ms.author: jeedes
ms.openlocfilehash: 1af0209265ec4945950120e80a83e19c8ab2eb4b
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99821859"
---
# <a name="tutorial-azure-active-directory-integration-with-snowflake"></a>자습서: Snowflake와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Snowflake를 통합하는 방법에 대해 알아봅니다. Azure AD와 Snowflake를 통합하면 다음 작업을 수행할 수 있습니다.

* Snowflake에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Snowflake에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

Snowflake와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 구할 수 있습니다.
* Snowflake Single Sign-On을 사용하도록 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

- Snowflake에서 **SP 및 IDP** 시작 SSO를 지원합니다.
- Snowflake가 [자동 사용자 프로비저닝 및 프로비전 해제](snowflake-provisioning-tutorial.md)(권장) 지원

## <a name="adding-snowflake-from-the-gallery"></a>갤러리에서 Snowflake 추가

Snowflake의 Azure AD 통합을 구성하려면 갤러리의 Snowflake를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Snowflake** 를 입력합니다.
1. 결과 패널에서 **Snowflake** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-snowflake"></a>Snowflake에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Snowflake에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Snowflake의 관련 사용자 간에 연결이 형성되어야 합니다.

Snowflake에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완성합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Snowflake SSO 구성](#configure-snowflake-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Snowflake 테스트 사용자 만들기](#create-snowflake-test-user)** - Azure AD 표현과 연결된 B.Simon에 해당하는 사용자를 Snowflake에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Snowflake** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

4. **IDP** 시작 모드에서 애플리케이션을 구성하려면 **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    a. **식별자** 텍스트 상자에서 `https://<SNOWFLAKE-URL>.snowflakecomputing.com` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://<SNOWFLAKE-URL>.snowflakecomputing.com/fed/login` 패턴을 사용하여 URL을 입력합니다.

1. SP 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 을 클릭하고 다음 단계를 수행합니다.

    a. **로그인 URL** 텍스트 상자에서 `https://<SNOWFLAKE-URL>.snowflakecomputing.com` 패턴을 사용하여 URL을 입력합니다.
    
    b. **로그아웃 URL** 텍스트 상자에 `https://<SNOWFLAKE-URL>.snowflakecomputing.com/fed/logout` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다. 이러한 값을 얻으려면 [Snowflake 클라이언트 지원 팀](https://support.snowflake.net/s/)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

4. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **인증서(Base64)** 를 다운로드한 다음, 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

6. **Snowflake 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Snowflake에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Snowflake** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-snowflake-sso"></a>Snowflake SSO 구성

1. 다른 웹 브라우저 창에서 Snowflake에 보안 관리자 권한으로 로그인합니다.

1. 페이지의 오른쪽 위에 있는 **프로필** 을 클릭하여 **역할 전환** 을 **ACCOUNTADMIN** 으로 설정합니다.

    > [!NOTE]
    > 이 작업은 오른쪽 위 모서리의 사용자 이름 아래에서 선택한 컨텍스트와는 별개입니다.
    
    ![Snowflake 관리자](./media/snowflake-tutorial/tutorial_snowflake_accountadmin.png)

1. **다운로드한 Base 64 인증서** 를 메모장에서 엽니다. “-----BEGIN CERTIFICATE-----”와 “-----END CERTIFICATE-----" 사이의 값을 복사한 후 아래의 **인증서** 옆에 있는 큰따옴표에 붙여 넣습니다. **ssoUrl** 에 Azure Portal에서 복사한 **로그인 URL** 값을 붙여 넣습니다. **모든 쿼리** 를 선택하고 **실행** 을 클릭합니다.

   ![Snowflake sql](./media/snowflake-tutorial/tutorial_snowflake_sql.png)

   ```
   use role accountadmin;
   alter account set saml_identity_provider = '{
   "certificate": "<Paste the content of downloaded certificate from Azure portal>",
   "ssoUrl":"<Login URL value which you have copied from the Azure portal>",
   "type":"custom",
   "label":"AzureAD"
   }';
   alter account set sso_login_page = TRUE;
   ```


### <a name="create-snowflake-test-user"></a>Snowflake 테스트 사용자 만들기

Azure AD 사용자가 Snowflake에 로그인할 수 있도록 하려면 해당 사용자를 Snowflake로 프로비전해야 합니다. Snowflake에서 프로비전 작업은 수동으로 수행됩니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. Snowflake에 보안 관리자 권한으로 로그인합니다.

2. 페이지의 오른쪽 위에 있는 **프로필** 을 클릭하여 **역할 전환** 을 **ACCOUNTADMIN** 으로 설정합니다.  

    ![Snowflake 관리자](./media/snowflake-tutorial/tutorial_snowflake_accountadmin.png)

3. 아래 SQL 쿼리를 실행하여 사용자를 만듭니다. 아래와 같이 "로그인 이름"이 워크시트의 Azure AD 사용자 이름으로 설정되어 있는지 확인합니다.

    ![Snowflake adminsql](./media/snowflake-tutorial/tutorial_snowflake_usersql.png)

    ```
    use role accountadmin;
    CREATE USER britta_simon PASSWORD = '' LOGIN_NAME = 'BrittaSimon@contoso.com' DISPLAY_NAME = 'Britta Simon';
    ```

### <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

#### <a name="sp-initiated"></a>SP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Snowflake 로그온 URL로 리디렉션됩니다.  

* Snowflake 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

#### <a name="idp-initiated"></a>IDP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭하면 SSO를 설정한 Snowflake에 자동으로 로그인됩니다. 

Microsoft 내 앱을 사용하여 모든 모드에서 애플리케이션을 테스트할 수도 있습니다. 내 앱에서 Snowflake 타일을 클릭하면 SP 모드로 구성된 경우 로그인 흐름을 시작하기 위해 애플리케이션 로그온 페이지로 리디렉션되고, IDP 모드로 구성된 경우에는 SSO를 설정한 Snowflake에 자동으로 로그인됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.


## <a name="next-steps"></a>다음 단계

Snowflake를 구성한 후에는 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 침입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법 알아보기](/cloud-app-security/proxy-deployment-aad)
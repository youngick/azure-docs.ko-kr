---
title: '자습서: Slack에 대한 사용자 프로비저닝 - Azure AD'
description: 사용자 계정을 Slack으로 자동으로 프로비전 및 프로비전 해제하도록 Azure Active Directory를 구성하는 방법을 알아봅니다.
services: active-directory
author: ArvindHarinder1
manager: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 05/06/2020
ms.author: arvinh
ms.openlocfilehash: 92c2ae13b840d7a73d86365ce88584bcafc878e8
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96181461"
---
# <a name="tutorial-configure-slack-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전을 위한 Slack 구성

이 자습서의 목적은 사용자 계정을 Azure AD에서 Slack으로 자동으로 프로비전 및 프로비전 해제하도록 Slack 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다. 이 서비스의 기능, 작동 방법 및 질문과 대답에 대한 중요한 내용은 [Azure Active Directory를 사용하여 SaaS 애플리케이션의 사용자를 자동으로 프로비저닝 및 프로비저닝 해제](../app-provisioning/user-provisioning.md)를 참조하세요. 


## <a name="capabilities-supported"></a>지원되는 기능
> [!div class="checklist"]
> * Slack에서 사용자 만들기
> * Slack에서 더 이상 액세스할 필요가 없는 사용자 제거
> * Azure AD와 Slack 간에 사용자 특성을 동기화된 상태로 유지
> * Slack에서 그룹 및 그룹 멤버 프로비저닝
> * Slack에 대한 [Single Sign-On](./slack-tutorial.md)(추천)


## <a name="prerequisites"></a>사전 요구 사항

이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.

* [Azure AD 테넌트](../develop/quickstart-create-new-tenant.md)
* 프로비저닝을 구성할 [권한](../roles/permissions-reference.md)이 있는 Azure AD의 사용자 계정(예: 애플리케이션 관리자, 클라우드 애플리케이션 관리자, 애플리케이션 소유자 또는 전역 관리자).
* [추가 플랜](https://aadsyncfabric.slack.com/pricing) 이상을 사용하도록 설정된 Slack 테넌트
* 팀 관리자 권한이 있는 Slack의 사용자 계정

## <a name="step-1-plan-your-provisioning-deployment"></a>1단계. 프로비저닝 배포 계획
1. [프로비저닝 서비스의 작동 방식](../app-provisioning/user-provisioning.md)에 대해 알아봅니다.
2. [프로비저닝 범위](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)에 있는 사용자를 결정합니다.
3. [Azure AD와 Slack 간에 매핑](../app-provisioning/customize-application-attributes.md)할 데이터를 결정합니다. 

## <a name="step-2-add-slack-from-the-azure-ad-application-gallery"></a>2단계. Azure AD 애플리케이션 갤러리에서 Slack 추가

Azure AD 애플리케이션 갤러리에서 Slack을 추가하여 Slack에 대한 프로비저닝 관리를 시작합니다. 이전에 SSO에 대해 Slack을 설정한 경우 동일한 애플리케이션을 사용할 수 있습니다. 그러나 처음 통합을 테스트하는 경우 별도의 앱을 만드는 것이 좋습니다. [여기](../manage-apps/add-application-portal.md)를 클릭하여 갤러리에서 애플리케이션을 추가하는 방법에 대해 자세히 알아봅니다. 

## <a name="step-3-define-who-will-be-in-scope-for-provisioning"></a>3단계. 프로비저닝 범위에 있는 사용자 정의 

Azure AD 프로비저닝 서비스를 사용하면 애플리케이션에 대한 할당 또는 사용자/그룹의 특성을 기반으로 프로비저닝되는 사용자의 범위를 지정할 수 있습니다. 할당을 기준으로 앱에 프로비저닝할 사용자의 범위를 선택하려면 다음 [단계](../manage-apps/assign-user-or-group-access-portal.md)를 사용하여 애플리케이션에 사용자 및 그룹을 할당할 수 있습니다. 사용자 또는 그룹의 특성만을 기준으로 프로비저닝할 사용자의 범위를 선택하려면 [여기](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md) 설명된 대로 범위 지정 필터를 사용할 수 있습니다. 

* 사용자 및 그룹을 Slack에 할당하는 경우 **기본 액세스** 이외의 역할을 선택해야 합니다. 기본 액세스 역할이 있는 사용자는 프로비저닝에서 제외되고 프로비저닝 로그에 실질적으로 권한을 부여받지 않은 것으로 표시됩니다. 애플리케이션에서 사용할 수 있는 유일한 역할이 기본 액세스 역할인 경우에는 [애플리케이션 매니페스트를 업데이트](../develop/howto-add-app-roles-in-azure-ad-apps.md)하여 역할을 더 추가할 수 있습니다. 

* 소규모로 시작합니다. 모든 사용자에게 배포하기 전에 소수의 사용자 및 그룹 집합으로 테스트합니다. 할당된 사용자 및 그룹으로 프로비저닝 범위가 설정된 경우 앱에 하나 또는 두 개의 사용자 또는 그룹을 할당하여 범위를 제어할 수 있습니다. 모든 사용자 및 그룹으로 범위가 설정된 경우 [특성 기반 범위 지정 필터](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)를 지정할 수 있습니다.

## <a name="step-4-configure-automatic-user-provisioning-to-slack"></a>4단계. Slack에 대한 자동 사용자 프로비저닝 구성 

이 섹션에서는 사용자의 Azure AD를 Slack의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Slack에서 할당된 사용자 계정을 만들고, 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.

### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a>Azure AD에서 Slack에 자동 사용자 계정 프로비전을 구성하려면 다음을 수행합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. **엔터프라이즈 애플리케이션**, **모든 애플리케이션** 을 차례로 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **Slack** 를 선택합니다.

    ![애플리케이션 목록의 Slack 링크](common/all-applications.png)

3. **프로비전** 탭을 선택합니다.

    ![프로비저닝 옵션이 호출된 관리 옵션의 스크린샷](common/provisioning.png)

4. **프로비전 모드** 를 **자동** 으로 설정합니다.

    ![자동 옵션이 호출된 프로비저닝 모드 드롭다운 목록의 스크린샷](common/provisioning-automatic.png)

5. **관리자 자격 증명** 섹션에서 **권한 부여** 를 클릭합니다. 그러면 새 브라우저 창에서 Slack 권한 부여 대화 상자가 열립니다.

    ![관리자 자격 증명 권한 부여 단추를 보여 주는 스크린샷](media/slack-provisioning-tutorial/authorization.png)


6. 새 창에서 팀 관리자 계정을 사용하여 Slack에 로그인합니다. 표시된 권한 부여 대화 상자에서 프로비전을 사용하도록 설정하려는 Slack 팀을 선택한 다음, **권한 부여** 를 선택합니다. 완료되면 Azure Portal로 돌아가서 프로비전 구성을 완료합니다.

    ![권한 부여 대화 상자](./media/slack-provisioning-tutorial/slackauthorize.png)

7. Azure Portal에서 **연결 테스트** 를 클릭하여 Azure AD가 Slack 앱에 연결되었는지 확인합니다. 연결에 실패하면 Slack 계정에 팀 관리자 권한이 있는지 확인하고 "권한 부여" 단계를 다시 시도합니다.

8. **알림 이메일** 필드에 프로비저닝 오류 알림을 받을 개인 또는 그룹의 메일 주소를 입력하고, **오류가 발생할 경우 메일 알림 보내기** 확인란을 선택합니다.

    ![알림 이메일](common/provisioning-notification-email.png)

9. **저장** 을 선택합니다.

10. 매핑 섹션에서 **Azure Active Directory 사용자를 Slack에 동기화** 를 선택합니다.

11. **특성 매핑** 섹션에서 Azure AD에서 Slack로 동기화할 사용자 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업 시 Slack의 사용자 계정을 일치시키는 데 사용됩니다. 저장 단추를 선택하여 변경 내용을 커밋합니다.

   |attribute|Type|
   |---|---|
   |활성|부울|
   |externalId|String|
   |displayName|String|
   |name.familyName|String|
   |name.givenName|String|
   |title|String|
   |emails[type eq "work"].value|String|
   |userName|String|
   |nickName|String|
   |addresses[type eq "untyped"].streetAddress|String|
   |addresses[type eq "untyped"].locality|String|
   |addresses[type eq "untyped"].region|String|
   |addresses[type eq "untyped"].postalCode|String|
   |addresses[type eq "untyped"].country|String|
   |phoneNumbers[type eq "mobile"].value|String|
   |phoneNumbers[type eq "work"].value|String|
   |roles[primary eq "True"].value|String|
   |locale|String|
   |name.honorificPrefix|String|
   |photos[type eq "photo"].value|String|
   |profileUrl|String|
   |timezone|String|
   |userType|String|
   |urn:scim:schemas:extension:enterprise:1.0.department|String|
   |urn:scim:schemas:extension:enterprise:1.0.manager|참조|
   |urn:scim:schemas:extension:enterprise:1.0.employeeNumber|String|
   |urn:scim:schemas:extension:enterprise:1.0.costCenter|String|
   |urn:scim:schemas:extension:enterprise:1.0.organization|String|
   |urn:scim:schemas:extension:enterprise:1.0.division|String|

12. **매핑** 섹션 아래에서 **Azure Active Directory 그룹을 Slack에 동기화** 를 선택합니다.

13. **특성 매핑** 섹션에서 Azure AD에서 Slack으로 동기화할 그룹 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업 시 Slack의 그룹을 일치시키는 데 사용됩니다. 저장 단추를 선택하여 변경 내용을 커밋합니다.

      |attribute|Type|
      |---|---|
      |displayName|String|
      |members|참조|

14. 범위 지정 필터를 구성하려면 [범위 지정 필터 자습서](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)에서 제공하는 다음 지침을 참조합니다.

15. Slack에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태** 를 **켜기** 로 변경합니다.

    ![프로비전 상태 켜기로 전환](common/provisioning-toggle-on.png)

16. **설정** 섹션의 **범위** 에서 원하는 값을 선택하여 Slack에 프로비저닝하려는 사용자 및/또는 그룹을 정의합니다.

    ![프로비전 범위](common/provisioning-scope.png)

17. 프로비전할 준비가 되면 **저장** 을 클릭합니다.

    ![프로비전 구성 저장](common/provisioning-configuration-save.png)

이 작업은 **설정** 의 **범위** 섹션에 정의된 모든 사용자 및/또는 그룹의 초기 동기화 주기를 시작합니다. 초기 주기는 Azure AD 프로비저닝 서비스가 실행되는 동안 약 40분마다 발생하는 후속 주기보다 더 많은 시간이 걸립니다. 

## <a name="step-5-monitor-your-deployment"></a>5단계. 배포 모니터링
프로비저닝을 구성한 후에는 다음 리소스를 사용하여 배포를 모니터링합니다.

1. [프로비저닝 로그](../reports-monitoring/concept-provisioning-logs.md)를 사용하여 어떤 사용자가 성공적으로 프로비저닝되었는지 확인합니다.
2. [진행률 표시줄](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user.md)을 통해 프로비저닝 주기 상태와 완료 정도를 확인합니다.
3. 프로비저닝 구성이 비정상 상태로 보이면 애플리케이션이 격리됩니다. 격리 상태에 대한 자세한 내용은 [여기](../app-provisioning/application-provisioning-quarantine-status.md)를 참조하세요.

## <a name="troubleshooting-tips"></a>문제 해결 팁

* Slack의 **displayName** 특성을 구성할 때는 다음 동작에 유의하세요.

  * 값이 완전히 고유하지는 않습니다(예: 2명의 사용자가 동일한 표시 이름을 가질 수 있음).

  * 비영어 문자, 공백, 대/소문자를 지원합니다. 
  
  * 허용되는 문장 부호에는 마침표, 밑줄, 하이픈, 아포스트로피, 대괄호(예: **( [ { } ] )**) 및 구분 기호(예: **, / ;**)가 포함됩니다.
  
  * displayName 속성에는 '\@' 문자를 사용할 수 없습니다. '\@'가 포함되면 프로비저닝 로그에서 "AttributeValidationFailed"라는 설명이 있는 건너뛴 이벤트를 찾을 수 있습니다.

  * Slack의 작업 공간/조직에서 두 설정, 즉 **Profile syncing is enabled**(프로필 동기화 사용) 및 **Users cannot change their display name**(사용자가 표시 이름을 변경할 수 없음)이 구성된 경우에만 업데이트됩니다.

* Slack의 **userName** 특성은 21자 미만이어야 하며 고유한 값을 가져야 합니다.

* Slack은 **userName** 및 **email** 특성과의 일치만 허용합니다.  
  
* 일반적인 오류 코드는 공식 Slack 설명서(https://api.slack.com/scim#errors )에서 설명하고 있습니다.

## <a name="change-log"></a>로그 변경

* 2020년 6월 16일 - 새 사용자를 만드는 동안에만 업데이트되도록 DisplayName 특성이 수정되었습니다.

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>다음 단계

* [프로비저닝 작업에 대한 로그를 검토하고 보고서를 받아보는 방법을 알아봅니다](../app-provisioning/check-status-user-account-provisioning.md).
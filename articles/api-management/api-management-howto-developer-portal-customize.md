---
title: 자습서 - 개발자 포털 액세스 및 사용자 지정 - Azure API Management | Microsoft Docs
description: 이 자습서에서는 API 설명서를 사용하여 원하는 대로 사용자 지정 가능한 자동 생성 웹 사이트인 API Management 개발자 포털을 사용자 지정하는 방법을 알아봅니다.
services: api-management
author: mikebudzynski
ms.service: api-management
ms.topic: tutorial
ms.date: 11/16/2020
ms.author: apimpm
ms.openlocfilehash: 90544fbafe7393630c3f3fbc694ae367eccb7f90
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96012983"
---
# <a name="tutorial-access-and-customize-the-developer-portal"></a>자습서: 개발자 포털 액세스 및 사용자 지정

*개발자 포털* 은 API 설명서를 사용하여 원하는 대로 사용자 지정 가능한 자동 생성 웹 사이트입니다. API 소비자는 API를 검색하고, API 사용 방법을 배우고, 액세스를 요청할 수 있습니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
> * 관리형 버전 개발자 포털에 액세스
> * 관리 인터페이스 탐색
> * 콘텐츠 사용자 지정
> * 변경 내용 게시
> * 게시된 포털 보기

개발자 포털에 대한 자세한 내용은 [Azure API Management 개발자 포털 개요](api-management-howto-developer-portal.md)를 참조하세요.

:::image type="content" source="media/api-management-howto-developer-portal-customize/cover.png" alt-text="API Management 개발자 포털 - 관리자 모드" border="false":::

## <a name="prerequisites"></a>사전 요구 사항

- 다음 빠른 시작을 완료합니다. [Azure API Management 인스턴스 만들기](get-started-create-service-instance.md)
- Azure API Management 인스턴스를 가져오고 게시합니다. 자세한 내용은 [가져오기 및 게시](import-and-publish.md)를 참조하세요.

[!INCLUDE [premium-dev-standard-basic.md](../../includes/api-management-availability-premium-dev-standard-basic.md)]

## <a name="access-the-portal-as-an-administrator"></a>관리자 권한으로 포털에 액세스

아래 단계에 따라 관리형 버전 포털에 액세스합니다.

1. [Azure Portal](https://portal.azure.com)에서 API Management 인스턴스로 이동합니다.
1. 위쪽 탐색 모음에서 **개발자 포털** 단추를 선택합니다. 관리형 버전 포털이 포함된 새 브라우저 탭이 열립니다.

## <a name="understand-the-portals-administrative-interface"></a>포털의 관리 인터페이스 이해

### <a name="default-content"></a>기본 콘텐츠 

포털에 처음으로 액세스하는 경우 기본 콘텐츠가 백그라운드에서 자동으로 프로비저닝됩니다. 기본 콘텐츠는 포털의 기능을 소개하고 포털을 개인 설정하는 데 필요한 사용자 지정을 최소화하도록 설계되었습니다. 포털 콘텐츠에 포함된 내용에 대한 자세한 정보는 [Azure API Management 개발자 포털 개요](api-management-howto-developer-portal.md)를 참조하세요.

### <a name="visual-editor"></a>시각적 개체 편집기

시각적 개체 편집기를 사용하여 포털의 콘텐츠를 사용자 지정할 수 있습니다. 
* 왼쪽의 메뉴 섹션에서는 페이지, 미디어, 레이아웃, 메뉴, 스타일 또는 웹 사이트 설정을 만들거나 수정할 수 있습니다. 
* 아래쪽의 메뉴 항목을 사용하면 뷰포트(예: 모바일 또는 데스크톱) 간에 전환하고, 인증된 사용자 또는 익명 사용자에게 표시되는 포털 요소를 살펴보고, 작업을 저장하거나 실행 취소할 수 있습니다.
* 더하기 기호가 있는 파란색 아이콘을 클릭하여 페이지에 행을 추가할 수 있습니다. 
* 위젯(예: 텍스트, 이미지 또는 API 목록)은 더하기 기호가 있는 회색 아이콘을 눌러 추가할 수 있습니다.
* 끌어서 놓기 상호 작용을 사용하여 페이지의 항목을 다시 정렬할 수 있습니다. 

### <a name="layouts-and-pages"></a>레이아웃 및 페이지

:::image type="content" source="media/api-management-howto-developer-portal-customize/pages-layouts.png" alt-text="페이지 및 레이아웃" border="false":::

레이아웃은 페이지가 표시되는 방식을 정의합니다. 예를 들어 기본 콘텐츠에는 두 가지 레이아웃이 있습니다. 하나는 홈 페이지에 적용되고, 다른 하나는 그 외의 모든 페이지에 적용됩니다.

레이아웃은 URL 템플릿을 페이지 URL과 매칭하여 페이지에 적용됩니다. 예를 들어 URL 템플릿이 `/wiki/*`인 레이아웃은 URL에 `/wiki/` 세그먼트가 포함된 모든 페이지에 적용됩니다(예: `/wiki/getting-started`, `/wiki/styles`).

위의 그림에서, 레이아웃에 속하는 콘텐츠는 파란색으로 표시되고 페이지는 빨강으로 표시됩니다. 메뉴 섹션은 각각 표시됩니다.

### <a name="styling-guide"></a>스타일 지정 가이드

:::image type="content" source="media/api-management-howto-developer-portal-customize/styling-guide.png" alt-text="스타일 지정 가이드" border="false":::

스타일 지정 가이드는 디자이너를 염두에 두고 고안된 패널입니다. 이 가이드를 통해 포털의 모든 시각적 요소를 감독하고 스타일을 지정할 수 있습니다. 스타일 지정은 계층적입니다. 많은 요소가 다른 요소의 속성을 상속합니다. 예를 들어 단추 요소는 텍스트와 배경에 색을 사용합니다. 단추의 색을 변경하려면 원래 색 변형을 변경해야 합니다.

변형을 편집하려면 변형을 선택하고 그 위에 표시되는 연필 아이콘을 선택합니다. 팝업 창에서 변경을 수행한 후 창을 닫습니다.

### <a name="save-button"></a>저장 단추

:::image type="content" source="media/api-management-howto-developer-portal-customize/save-button.png" alt-text="저장 단추" border="false":::

포털에서 변경 작업을 수행할 때마다 아래쪽의 메뉴에서 **저장** 단추를 선택하거나 [Ctrl]+[S]를 눌러 수동으로 저장해야 합니다. 변경 내용을 저장하면 수정된 콘텐츠가 API Management 서비스에 자동으로 업로드됩니다.

## <a name="customize-the-portals-content"></a>포털 콘텐츠 사용자 지정

포털을 방문자에게 개방하기 전에, 자동으로 생성된 콘텐츠를 개인 설정해야 합니다. 홈페이지의 레이아웃, 스타일, 콘텐츠 등을 변경하는 것이 좋습니다.

> [!NOTE]
> 통합을 고려해야 하기 때문에 `/404`, `/500`, `/captcha`, `/change-password`, `/config.json`, `/confirm/invitation`, `/confirm-v2/identities/basic/signup`, `/confirm-v2/password`, `/internal-status-0123456789abcdef`, `/publish`, `/signin`, `/signin-sso`, `/signup` 페이지를 제거하거나 다른 URL로 이동할 수 없습니다.

### <a name="home-page"></a>홈 페이지

기본 **홈** 페이지는 자리 표시자 콘텐츠로 채워집니다. 이 콘텐츠가 들어 있는 전체 섹션을 제거할 수도 있고, 구조를 유지하면서 요소를 하나씩 조정할 수도 있습니다. 생성된 텍스트와 이미지를 개발자의 텍스트와 이미지로 바꾸고 링크가 원하는 위치를 가리키는지 확인합니다.

### <a name="layouts"></a>레이아웃

탐색 모음의 자동으로 생성된 로고를 개발자 고유의 이미지로 바꿉니다.

### <a name="styling"></a>스타일 지정

스타일을 반드시 조정해야 하는 것은 아니지만 특정 요소를 조정해야 할 수 있습니다. 예를 들어 브랜드 색과 일치하도록 기본 색을 변경할 수 있습니다.

### <a name="customization-example"></a>사용자 지정 예제

다음 비디오에서는 포털의 콘텐츠를 편집하고, 웹 사이트의 모양을 사용자 지정하고, 변경 내용을 게시하는 방법을 보여줍니다.

> [!VIDEO https://www.youtube.com/embed/5mMtUSmfUlw]

## <a name="publish-the-portal"></a><a name="publish"></a> 포털 게시

포털과 포털의 최신 변경 내용을 방문자에게 제공하려면 포털을 *게시* 해야 합니다. 포털의 관리 인터페이스 내에서 또는 Azure Portal에서 포털을 게시할 수 있습니다.

### <a name="publish-from-the-administrative-interface"></a>관리 인터페이스에서 게시

1. **저장** 아이콘을 선택하여 변경 내용을 저장했는지 확인합니다.
1. 메뉴의 **작업** 섹션에서 **웹 사이트 게시** 를 선택합니다. 이 작업은 몇 분 정도 걸릴 수 있습니다.  

    :::image type="content" source="media/api-management-howto-developer-portal-customize/publish-portal.png" alt-text="포털 게시" border="false":::

### <a name="publish-from-the-azure-portal"></a>Azure Portal에서 게시

1. [Azure Portal](https://portal.azure.com)에서 API Management 인스턴스로 이동합니다.
1. 왼쪽 메뉴의 **개발자 포털** 에서 **포털 개요** 를 선택합니다.
1. **포털 개요** 창에서 **게시** 를 선택합니다.

    :::image type="content" source="media/api-management-howto-developer-portal-customize/pubish-portal-azure-portal.png" alt-text="Azure Portal에서 포털 게시":::

> [!NOTE]
> API Management 서비스 구성이 변경되면 포털을 다시 게시해야 합니다. 예를 들어 사용자 지정 도메인을 할당하거나, ID 공급자를 업데이트하거나, 위임을 설정하거나, 로그인 및 제품 사용 약관을 지정한 후에는 포털을 다시 게시해야 합니다.


## <a name="visit-the-published-portal"></a>게시된 포털 방문

포털을 게시한 후에는 관리 패널과 동일한 URL(예: `https://contoso-api.developer.azure-api.net`)에서 포털에 액세스할 수 있습니다. 별도의 브라우저 세션에서(Incognito 또는 프라이빗 검색 모드 사용) 외부 방문자로 포털을 살펴봅니다.

## <a name="apply-the-cors-policy-on-apis"></a>API에 CORS 정책 적용

포털 방문자가 기본 제공 대화형 콘솔을 통해 API를 테스트할 수 있게 하려면 API에서 CORS(원본 간 리소스 공유)를 사용하도록 설정합니다. 자세한 내용은 [Azure API Management 개발자 포털 개요](api-management-howto-developer-portal.md#cors)를 참조하세요.

## <a name="next-steps"></a>다음 단계

다음 문서를 통해 개발자 포털에 대해 자세히 알아봅니다.

- [Azure API Management 개발자 포털 개요](api-management-howto-developer-portal.md)
- 더 이상 사용되지 않는 레거시 포털에서 [새 개발자 포털로 마이그레이션](developer-portal-deprecated-migration.md)합니다.
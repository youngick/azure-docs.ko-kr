---
title: '자습서: Azure Static Web Apps에서 Blazor를 사용하여 정적 웹앱 빌드'
description: Blazor를 사용하여 Azure Static Web Apps 웹 사이트를 빌드하는 방법을 알아봅니다.
services: static-web-apps
author: craigshoemaker
ms.service: static-web-apps
ms.topic: tutorial
ms.date: 09/10/2020
ms.author: cshoe
ms.openlocfilehash: 0086f7f68fd05d6925d19c7ab457fbc125e36be4
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96350231"
---
# <a name="tutorial-building-a-static-web-app-with-blazor-in-azure-static-web-apps"></a>자습서: Azure Static Web Apps에서 Blazor를 사용하여 정적 웹앱 빌드

Azure Static Web Apps는 GitHub 리포지토리에서 앱을 빌드하여 프로덕션 환경에 웹 사이트를 게시합니다. 이 자습서에서는 Azure Portal을 사용하여 웹 애플리케이션을 Azure Static 웹앱에 배포합니다.

Azure 구독이 아직 없는 경우 [평가판 계정](https://azure.microsoft.com/free)을 만듭니다.

## <a name="prerequisites"></a>필수 구성 요소

- [GitHub](https://github.com) 계정
- [Azure](https://portal.azure.com) 계정

## <a name="application-overview"></a>애플리케이션 개요

Azure Static Web Apps를 사용하면 서버리스 백 엔드에서 지원하는 정적 웹 애플리케이션을 만들 수 있습니다. 다음 자습서에서는 날씨 데이터를 반환하는 C# Blazor 웹 애플리케이션을 배포하는 방법을 보여줍니다.

:::image type="content" source="./media/deploy-blazor/blazor-app-complete.png" alt-text="완전한 Blazor 앱":::

이 자습서에서 사용하는 앱은 다음과 같은 세 가지 Visual Studio 프로젝트로 구성됩니다.

- **Api**: 정적 앱에 날씨 정보를 제공하는 API 엔드포인트를 구현하는 C# Azure Functions 애플리케이션입니다. **WeatherForecastFunction** 은 `WeatherForecast` 개체의 배열을 반환합니다.

- **클라이언트**: 프런트 엔드 Blazor 웹 어셈블리 프로젝트입니다. 모든 경로에 _index.html_ 파일이 제공되도록 [대체(fallback) 경로](#fallback-route)가 구현됩니다.

- **공유**: API 엔드포인트에서 프런트 엔드 웹앱으로 데이터가 흐를 수 있도록 API 프로젝트와 클라이언트 프로젝트에서 모두 참조하는 공통 클래스를 보관합니다. [`WeatherForecast`](https://github.com/staticwebdev/blazor-starter/blob/main/Shared/WeatherForecast.cs) 클래스는 두 앱 간에 공유됩니다.

이러한 프로젝트는 API 백 엔드에서 지원하는 브라우저에서 실행되는 Blazor 웹 어셈블리 애플리케이션을 만드는 데 필요한 파트를 구성합니다.

## <a name="fallback-route"></a>대체(fallback) 경로

애플리케이션은 애플리케이션의 특정 경로에 매핑되는 _/counter_ 및 _/fetchdata_ 같은 URL을 공개합니다. 이 앱은 단일 페이지 애플리케이션으로 구현되기 때문에 각 경로에 _index.html_ 파일이 제공됩니다. 모든 경로 요청에서 _index.html_ 을 반환하도록 클라이언트 프로젝트의 _wwwroot_ 폴더에 있는 _routes.json_ 파일에 [대체(fallback) 경로](./routes.md#fallback-routes)가 구현됩니다.

```json
{
  "routes": [
    {
      "route": "/*",
      "serve": "/index.html",
      "statusCode": 200
    }
  ]
}
```

위와 같이 구성하면 앱의 모든 경로 요청에서 _index.html_ 페이지를 반환합니다.

## <a name="create-a-repository"></a>리포지토리 만들기

이 문서에서는 GitHub 템플릿 리포지토리를 사용하여 쉽게 시작할 수 있습니다. 이 템플릿에는 Azure Static Web Apps에 배포되는 스타터 앱이 있습니다.

1. GitHub에 로그인했는지 확인하고 다음 위치로 이동하여 새 리포지토리를 만듭니다.
    - [https://github.com/staticwebdev/blazor-starter/generate](https://github.com/login?return_to=/staticwebdev/blazor-starter/generate)
1. 리포지토리 이름을 **my-first-static-blazor-app** 으로 지정합니다.

## <a name="create-a-static-web-app"></a>정적 웹앱 만들기

이제 리포지토리가 생성되었으므로 Azure Portal에서 정적 웹앱을 만듭니다.

1. [Azure Portal](https://portal.azure.com)로 이동합니다.
1. **리소스 만들기** 선택
1. **Static Web Apps** 를 검색합니다.
1. **Static Web Apps(미리 보기)** 선택
1. **만들기** 를 선택합니다.

_기본 사항_ 섹션에서 새 앱을 구성하고 GitHub 리포지토리에 연결하여 시작합니다.

:::image type="content" source="media/deploy-blazor/basics.png" alt-text="기본 사항 탭":::

1. _Azure 구독_ 선택
1. 새 _리소스 그룹_ 선택 또는 만들기
1. 앱 이름을 **my-first-static-blazor-app** 으로 지정합니다.
    - 유효한 문자는 `a-z`(대/소문자 구분 안 함), `0-9`및 `-`입니다.
1. 가장 가까운 _지역_ 을 선택합니다.
1. **무료** _SKU_ 를 선택합니다.
1. **GitHub로 로그인** 단추를 선택하고 GitHub로 인증합니다.

GitHub로 로그인한 후 리포지토리 정보를 입력합니다.

:::image type="content" source="media/deploy-blazor/repository-details.png" alt-text="리포지토리 세부 정보":::

1. 원하는 _조직_ 을 선택합니다.
1. _리포지토리_ 드롭다운에서 **my-first-static-blazor-app** 을 선택합니다.
1. _분기_ 드롭다운에서 **주** 를 선택합니다.

    리포지토리가 표시되지 않는 경우 GitHub에서 Azure Static Web Apps에 권한을 부여해야 할 수 있습니다. GitHub 리포지토리로 이동하여 **설정 > 애플리케이션 > 권한 부여된 OAuth 앱** 으로 이동하고 **Azure Static Web Apps** 를 선택한 다음 **권한 부여** 를 선택합니다. 조직 리포지토리의 경우 사용 권한을 부여하려면 조직의 소유자여야 합니다.

1. _빌드 세부 정보_ 섹션에서 Blazor 관련 구성 세부 정보를 추가합니다.

    - _빌드 사전 설정_ 드롭다운에서 **Blazor** 를 선택하고 모든 기본값을 유지합니다.

1. **검토 + 만들기** 를 선택합니다.

    :::image type="content" source="media/deploy-blazor/review-create.png" alt-text="만들기 단추 검토":::

1. **만들기** 를 선택합니다.

    :::image type="content" source="media/deploy-blazor/create-button.png" alt-text="만들기 단추":::

1. **리소스로 이동** 을 선택합니다.

    :::image type="content" source="media/deploy-blazor/resource-button.png" alt-text="리소스로 이동 단추":::

## <a name="view-the-website"></a>웹 사이트 보기

정적 앱을 배포하는 데는 두 가지 측면이 있습니다. 첫 번째는 앱을 구성하는 기본 Azure 리소스를 프로비저닝합니다. 두 번째는 애플리케이션을 빌드하고 게시하는 GitHub Actions 워크플로입니다.

새 정적 사이트로 이동하려면 먼저 배포 빌드가 실행을 완료해야 합니다.

Static Web Apps 개요 창에는 웹앱과 상호 작용하는 데 도움이 되는 일련의 링크가 표시됩니다.

:::image type="content" source="./media/deploy-blazor/overview-window.png" alt-text="개요 창":::

1. _GitHub Actions 실행 상태를 확인하려면 여기를 클릭하세요._ 라는 배너를 클릭하면 리포지토리에 대해 실행 중인 GitHub Actions로 이동됩니다. 배포 작업이 완료되었는지 확인되면 생성된 URL을 통해 웹 사이트로 이동할 수 있습니다.

2. GitHub Actions 워크플로가 완료되면 _URL_ 링크를 선택하여 새 탭에서 웹 사이트를 열 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

이 애플리케이션을 계속 사용하지 않을 경우 다음 단계를 통해 Azure Static Web App 인스턴스를 삭제할 수 있습니다.

1. [Azure Portal](https://portal.azure.com)을 엽니다.
1. 위쪽 검색 창에서 **my-first-static-blazor-app** 을 검색합니다.
1. 앱 이름을 선택합니다.
1. **삭제** 단추를 선택합니다.
1. **예** 를 선택하여 삭제 작업을 확인합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [인증 및 권한 부여](./authentication-authorization.md)

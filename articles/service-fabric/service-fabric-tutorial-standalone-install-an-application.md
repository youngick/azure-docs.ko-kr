---
title: 독립 실행형 클러스터에 앱 설치
description: 이 자습서에서는 독립 실행형 Service Fabric 클러스터에 애플리케이션을 설치하는 방법을 알아봅니다.
ms.topic: tutorial
ms.date: 07/22/2019
ms.custom: mvc
ms.openlocfilehash: ae946321b34f12c816a717db4a3d07f57feefe52
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96485363"
---
# <a name="tutorial-deploy-an-application-on-your-service-fabric-standalone-cluster"></a>자습서: Service Fabric 독립 실행형 클러스터에 애플리케이션 배포

Service Fabric 독립 실행형 클러스터는 사용자 자신의 환경을 선택하고 Service Fabric이 수행하는 "모든 OS 및 모든 클라우드" 접근 방법의 일부로서 클러스터를 만드는 옵션을 제공합니다. 이 자습서 시리즈에서는 AWS에서 호스팅되는 독립 실행형 클러스터를 만들고 여기에 애플리케이션을 배포합니다.

이 자습서는 시리즈의 3부입니다.  Service Fabric 독립 실행형 클러스터는 사용자 자신의 환경을 선택하고 Service Fabric을 사용하여 “모든 OS 및 모든 클라우드” 접근 방법의 일부로서 클러스터를 만드는 옵션을 제공합니다. 이 자습서에서는 이 독립 실행형 클러스터를 호스트하는 데 필요한 AWS 인프라를 만드는 방법을 보여 줍니다.

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 샘플 앱 다운로드
> * 클러스터에 배포

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 시작하기 전에:

* [Visual Studio 2019를 설치](https://www.visualstudio.com/)하고 **Azure 개발** 과 **ASP.NET 및 웹 개발** 워크로드를 설치합니다.
* [Service Fabric SDK를 설치](service-fabric-get-started.md)합니다.

## <a name="download-the-voting-sample-application"></a>투표 애플리케이션 샘플 다운로드

명령 창에서 다음 명령을 실행하여 로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

### <a name="deploy-the-app-to-the-service-fabric-cluster"></a>Service Fabric 클러스터에 앱 배포

애플리케이션이 다운로드되면 Visual Studio에서 클러스터에 직접 배포할 수 있습니다.

1. Visual Studio 열기

2. **파일** > **열기** 선택

3. Git 리포지토리를 복제한 폴더로 이동해 Voting.sln을 선택

4. 솔루션 탐색기에서 `Voting` 애플리케이션 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시** 선택

5. **연결 엔드포인트** 에 대한 드롭다운을 선택하고 클러스터에서 노드 중 하나의 공용 DNS 이름을 입력합니다.  `ec2-34-215-183-77.us-west-2.compute.amazonaws.com:19000`)을 입력합니다. Azure에서는 FQDN(정규화된 도메인 이름)이 자동으로 제공되지 않지만 쉽게 [VM 개요 페이지에서 설정](../virtual-machines/create-fqdn.md)할 수 있습니다.

6. 기본 설정 브라우저 및 유형을 클러스터 주소(이 앱이 포트 8080에 배포하는 연결 엔드포인트 - 예를 들어 ec2-34-215-183-77.us-west-2.compute.amazonaws.com:8080)를 엽니다.

    ![클러스터에서 API 응답](./media/service-fabric-tutorial-standalone-cluster/deployed-app.png)

## <a name="next-steps"></a>다음 단계

이 문서에서는 클러스터에 애플리케이션을 배포하는 방법을 알아보았습니다.

> [!div class="checklist"]
> * 샘플 앱 다운로드
> * 클러스터에 배포

클러스터를 정리하려면 시리즈의 4부로 이동합니다.

> [!div class="nextstepaction"]
> [리소스 정리](service-fabric-tutorial-standalone-clean-up.md)
---
title: 포함 파일
description: 포함 파일
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: include
ms.date: 08/04/2020
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 404fd10c3e3610671d2b6e5dbc6aba8bcaa70046
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "100019579"
---
## <a name="push-image-to-registry"></a>레지스트리에 이미지 푸시

Azure Container Registry에 이미지를 푸시하려면 먼저 이미지가 있어야 합니다. 로컬 컨테이너 이미지가 아직 없는 경우 다음 [docker pull][docker-pull] 명령을 실행하여 기존 퍼블릭 이미지를 끌어옵니다. 이 예제에서는 Microsoft Container Registry에서 `hello-world` 이미지를 끌어옵니다.

```
docker pull mcr.microsoft.com/hello-world
```

레지스트리에 이미지를 푸시하기 전에 레지스트리 로그인 서버의 정규화된 이름을 사용하여 태그를 지정해야 합니다. 로그인 서버 이름은 *\<registry-name\>.azurecr.io*(모두 소문자여야 함) 형식입니다(예: *mycontainerregistry.azurecr.io*).

[docker tag][docker-tag] 명령을 사용하여 이미지에 태그를 지정합니다. `<login-server>`를 ACR 인스턴스의 로그인 서버 이름으로 바꿉니다.

```
docker tag mcr.microsoft.com/hello-world <login-server>/hello-world:v1
```

예제:

```
docker tag mcr.microsoft.com/hello-world mycontainerregistry.azurecr.io/hello-world:v1
```


마지막으로 [docker push][docker-push]를 사용하여 레지스트리 인스턴스로 이미지를 푸시합니다. `<login-server>`를 레지스트리 인스턴스의 로그인 서버 이름으로 바꿉니다. 이 예제에서는 `hello-world:v1` 이미지를 포함하는 **hello-world** 리포지토리를 만듭니다.

```
docker push <login-server>/hello-world:v1
```

이미지를 컨테이너 레지스트리에 푸시한 후에는 로컬 Docker 환경에서 `hello-world:v1` 이미지를 제거합니다. (이 [docker rmi][docker-rmi] 명령은 Azure 컨테이너 레지스트리의 **hello-world** 리포지토리에서 이미지를 제거하지 않습니다.)

```
docker rmi <login-server>/hello-world:v1
```

<!-- LINKS - External -->
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-pull]: https://docs.docker.com/engine/reference/commandline/pull/
[docker-rmi]: https://docs.docker.com/engine/reference/commandline/rmi/
[docker-run]: https://docs.docker.com/engine/reference/commandline/run/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/

<!-- LINKS - Internal -->


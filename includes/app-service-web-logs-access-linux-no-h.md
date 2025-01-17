---
title: 파일 포함
description: 포함 파일
services: app-service
author: cephalin
ms.service: app-service
ms.topic: include
ms.date: 03/27/2019
ms.author: cephalin
ms.custom: include file
ms.openlocfilehash: df71f0804b62eb4b17ff8d2f652b076b5c64c959
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92743783"
---
컨테이너 내부에서 생성된 콘솔 로그에 액세스할 수 있습니다.

먼저 다음 명령을 실행하여 컨테이너 로깅을 설정합니다.

```azurecli-interactive
az webapp log config --name <app-name> --resource-group <resource-group-name> --docker-container-logging filesystem
```

`<app-name>` 및 `<resource-group-name>`을 웹앱에 적합한 이름으로 바꿉니다.

컨테이너 로깅이 설정되면 다음 명령을 실행하여 로그 스트림을 확인합니다.

```azurecli-interactive
az webapp log tail --name <app-name> --resource-group <resource-group-name>
```

콘솔 로그가 즉시 표시되지 않으면 30초 후에 다시 확인합니다.

언제든지 로그 스트리밍을 중지하려면 **Ctrl**+**C** 를 입력합니다.

`https://<app-name>.scm.azurewebsites.net/api/logs/docker`의 브라우저에서 로그 파일을 검사할 수도 있습니다.

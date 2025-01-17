---
title: Media Services에서 표준 인코더를 사용 하 여 비디오 인코딩
description: 이 항목은 Media Services의 표준 인코더를 사용하여 입력 해상도 및 비트 전송률을 기반으로 자동 생성된 비트 전송률 사다리로 입력 비디오를 인코딩하는 방법을 보여줍니다.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/31/2020
ms.author: inhenkel
ms.custom: seodec18
ms.openlocfilehash: 5b973d17e10f3dbb75f5208d9003b4f8118b37c7
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98891406"
---
#  <a name="encode-with-an-auto-generated-bitrate-ladder"></a>자동 생성된 비트 전송률 사다리로 인코딩

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

## <a name="overview"></a>개요

이 문서는 Media Services의 표준 인코더를 사용하여 입력 해상도 및 비트 전송률을 기반으로 자동 생성된 비트 전송률 사다리로 입력 비디오를 인코딩하는 방법을 설명합니다. 이 기본 제공 인코더 설정 또는 사전 설정은 입력 해상도 및 비트 전송률을 결코 초과하지 않습니다. 예를 들어, 입력이 3Mbps에서 720p이고 출력이 최적 시 720p로 유지되는 경우 3Mbps보다 낮은 전송률로 시작됩니다.

### <a name="encoding-for-streaming"></a>스트리밍용 인코딩

**변환** 에서 **AdaptiveStreaming** 사전 설정을 사용하면 HLS 및 DASH와 같은 스트리밍 프로토콜을 통한 전달에 적합한 출력을 얻을 수 있습니다. 이 사전 설정을 사용할 때 서비스는 생성할 비디오 레이어 수와 비트 전송률 및 해상도를 지능적으로 결정합니다. 출력 콘텐츠에는 AAC 인코딩 오디오 및 H.264 인코딩 비디오가 인터리빙되지 않은 MP4 파일이 포함됩니다.

이 사전 설정이 사용된 예를 보려면 [파일 스트리밍](stream-files-dotnet-quickstart.md)을 참조하세요.

## <a name="output"></a>출력

이 섹션에서는 **AdaptiveStreaming** 사전 설정으로 인코딩한 결과로 Media Services 인코더에 의해 생성된 출력 계층의 세 가지 예를 보여 줍니다. 모든 경우에 출력에는 128kbps로 인코딩된 스테레오 오디오와 오디오 전용 MP4 파일이 포함됩니다.

### <a name="example-1"></a>예 1
높이가 "1080"이고 프레임 속도가 "29.970"인 원본은 6개의 비디오 계층을 생성합니다.

|계층|높이|너비|비트 전송률(kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>예제 2
높이가 "720"이고 프레임 속도가 "23.970"인 원본은 5개의 비디오 계층을 생성합니다.

|계층|높이|너비|비트 전송률(kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>예제 3
높이가 "360"이고 프레임 속도가 "29.970"인 원본은 3개의 비디오 계층을 생성합니다.

|계층|높이|너비|비트 전송률(kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [파일 스트리밍](stream-files-dotnet-quickstart.md)

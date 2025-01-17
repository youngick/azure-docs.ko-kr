---
title: Azure Media Services에서 대기 시간이 짧은 라이브 설정
description: 이 항목에서는 대기 시간이 짧은 라이브 설정에 대해 간략하게 설명 하 고 짧은 대기 시간을 설정 하는 방법을 보여 줍니다.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: conceptual
ms.date: 08/31/2020
ms.author: inhenkel
ms.custom: devx-track-csharp
ms.openlocfilehash: f9f4476e932df9a5f4c093968b2e7c4840e7ff39
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102122904"
---
# <a name="live-event-low-latency-settings"></a>라이브 이벤트 낮은 대기 시간 설정

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

이 문서에서는 [라이브 이벤트](/rest/api/media/liveevents)에서 짧은 대기 시간을 설정하는 방법을 보여줍니다. 또한 다양한 플레이어에서 짧은 대기 시간 설정을 사용하는 경우 표시되는 일반적인 결과에 대해 설명합니다. 그 결과는 CDN 및 네트워크 대기 시간에 따라 다릅니다.

새로운 **LowLatency** 기능을 사용하려면 **LiveEvent** 에서 **StreamOptionsFlag** 를 **LowLatency** 로 설정할 수 있습니다. HLS 재생에 대한 [LiveOutput](/rest/api/media/liveoutputs)을 만들 때 [LiveOutput.Hls.fragmentsPerTsSegment](/rest/api/media/liveoutputs/create#hls)를 1로 설정합니다. 스트림이 실행 되 면 [Azure Media Player](https://ampdemo.azureedge.net/) (AMP 데모 페이지)를 사용 하 고 재생 옵션을 "짧은 대기 시간 추론 프로필"을 사용 하도록 설정할 수 있습니다.

> [!NOTE]
> 현재 Azure Media Player의 LowLatency HeuristicProfile은 CSF 또는 CMAF 형식 (예: 또는)을 사용 하 여 MPEG-2 프로토콜의 스트림을 재생 하기 위한 것입니다 `format=mdp-time-csf` `format=mdp-time-cmaf` . 

다음 .NET 예제에서는 **LiveEvent** 에서 **LowLatency** 를 설정하는 방법을 보여줍니다.

[!code-csharp[Main](../../../media-services-v3-dotnet/Live/LiveEventWithDVR/Program.cs#NewLiveEvent)]

전체 예: [DVR를 사용 하는 라이브 이벤트](https://github.com/Azure-Samples/media-services-v3-dotnet/blob/main/Live/LiveEventWithDVR/Program.cs)를 참조 하세요.

## <a name="live-events-latency"></a>라이브 이벤트 대기 시간

다음 표는 기여 피드가 서비스에 도달하는 시점부터 뷰어가 플레이어에서 재생을 확인하는 시점 사이를 측정한 Media Services의 일반적인 대기 시간 결과를 보여줍니다(LowLatency 플래그를 사용하는 경우). 짧은 대기 시간을 사용하려면 인코더 설정을 1초 GOP(Group of Pictures) 길이로 조정해야 합니다. 더 높은 GOP 길이를 사용하면 동일한 프레임에서 대역폭 사용량이 최소화되고 비트 전송률이 낮아집니다. 움직임이 많지 않은 비디오에 특히 유용합니다.

### <a name="pass-through"></a>통과 

||2초 GOP 짧은 대기 시간 사용|1초 GOP 짧은 대기 시간 사용|
|---|---|---|
|**AMP의 DASH**|10초|8초|
|**기본 iOS 플레이어의 HLS**|14초|10초|

### <a name="live-encoding"></a>라이브 인코딩

||2초 GOP 짧은 대기 시간 사용|1초 GOP 짧은 대기 시간 사용|
|---|---|---|
|**AMP의 DASH**|14초|10초|
|**기본 iOS 플레이어의 HLS**|18초|13초|

> [!NOTE]
> 로컬 네트워크 조건에 따라 또는 CDN 캐싱 계층을 도입하여 엔드투엔드 대기 시간이 달라질 수 있습니다. 정확한 구성을 테스트해야 합니다.

## <a name="next-steps"></a>다음 단계

- [라이브 스트리밍 개요](live-streaming-overview.md)
- [라이브 스트리밍 자습서](stream-live-tutorial-with-api.md)

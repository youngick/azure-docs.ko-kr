---
title: Azure Media Services의 할당량 및 제한
description: 이 항목에서는 Microsoft Azure Media Services의 할당량 및 제한 사항에 대해 설명 합니다.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 10/23/2020
ms.author: inhenkel
ms.openlocfilehash: d6ca7a444f2a3d4babe220548edb10bd37784be7
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92678115"
---
<!-- If you update limits in this topic, make sure to also update https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits#media-services-limits -->
# <a name="azure-media-services-quotas-and-limits"></a>할당량 및 한도 Azure Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

이 문서에는 할당량이 라고도 하는 가장 일반적인 Microsoft Azure Media Services 제한 중 일부가 나열 되어 있습니다.

> [!NOTE]
> 고정되지 않은 리소스의 경우 지원 티켓을 열어 할당량 증가를 요청하세요. 더 높은 한도를 얻기 위해 추가 Azure Media Services 계정을 만들지 마세요.

## <a name="account-limits"></a>계정 제한

| 리소스 | 기본 제한 |
| --- | --- |
| 단일 구독의 [Media Services 계정](media-services-account-concept.md) | 100(고정) |

## <a name="asset-limits"></a>자산 제한

| 리소스 | 기본 제한 |
| --- | --- |
| Media Services 계정 당 [자산](assets-concept.md) | 1,000,000|

## <a name="storage-limits"></a>스토리지 제한

| 리소스 | 기본 제한 | 
| --- | --- | 
| 파일 크기| 일부 시나리오에서는 Media Services에서 처리를 위해 지원되는 최대 파일 크기에 제한이 있습니다. <sup>(1)</sup> |
| [스토리지 계정](storage-account-concept.md) | 100<sup>(2)</sup>(고정) |

<sup>1</sup> 현재 Azure Blob Storage에서 단일 blob에 대해 지원되는 최대 크기는 최대 5TB입니다. 서비스에서 사용되는 VM 크기에 따라 Media Services에 추가 제한이 적용됩니다. 크기 제한은 업로드하는 파일과 Media Services 처리(인코딩 또는 분석)의 결과로 생성되는 파일에도 적용됩니다. 원본 파일이 260GB보다 크면 작업이 실패할 수 있습니다. 

다음 표에서는 각 미디어 예약 단위 S1, S2 및 S3에 대한 제한을 보여줍니다. 원본 파일이 표에 정의된 제한보다 크면 인코딩 작업이 실패합니다. 4K 해상도 원본을 오랜 기간 인코딩하는 경우 필요한 성능을 얻기 위해 S3 미디어 예약 단위를 사용해야 합니다. S3 미디어 예약 단위에서 260GB 제한보다 큰 4K 콘텐츠가 있는 경우 지원 티켓을 엽니다.

|미디어 예약 단위 유형|최대 입력 크기(GB)|
|---|---|
|S1 |    26|
|S2    | 60|
|S3    |260|

<sup>2</sup> 스토리지 계정은 동일한 Azure 구독에 속해 있어야 합니다.

## <a name="jobs-encoding--analyzing-limits"></a>작업(인코딩 및 분석) 제한

| 리소스 | 기본 제한 | 
| --- | --- | 
| Media Services 계정 당 [작업](transforms-jobs-concept.md) | 500,000 <sup>(3)</sup>(고정)|
| 작업당 작업 입력 | 50(고정)|
| 작업당 작업 출력 | 20(고정) |
| Media Services 계정 당 [변환](transforms-jobs-concept.md) 수 | 100(고정)|
| 변환에서 출력 변환 | 20(고정) |
| 작업 입력당 파일|10(고정)|

<sup>3</sup> 이 번호에는 대기 중, 완료, 활성 및 취소된 작업도 포함됩니다. 삭제된 작업은 포함되지 않습니다. 

레코드의 총 수가 최고 할당량 미만인 경우에도 사용자 계정에 있는 90일이 지난 작업 레코드는 자동으로 삭제됩니다. 

## <a name="live-streaming-limits"></a>라이브 스트리밍 제한

| 리소스 | 기본 제한 | 
| --- | --- | 
| Media Services 계정 당 [라이브 이벤트](live-events-outputs-concept.md) <sup>(4)</sup> |5|
| 라이브 이벤트당 라이브 출력 |3<sup>(5)</sup> |
| 최대 라이브 출력 기간 | [DVR 창의 크기](live-event-cloud-dvr.md) |

<sup>4</sup> 라이브 이벤트 제한에 대 한 자세한 내용은 [라이브 이벤트 유형 비교 및 제한](live-event-types-comparison.md)을 참조 하세요.

<sup>5</sup> 라이브 출력은 생성과 동시에 시작되고 삭제되면 중지됩니다.

## <a name="packaging--delivery-limits"></a>패키징 및 전달 제한

| 리소스 | 기본 제한 |
| --- | --- |
| Media Services 계정에 따라 [스트리밍 끝점](streaming-endpoint-concept.md) (중지 됨 또는 실행 중) | 2 |
| 프리미엄 스트리밍 단위 | 10 |
| [동적 매니페스트 필터](filters-dynamic-manifest-overview.md)|100|
| [스트리밍 정책](streaming-policy-concept.md) | 100<sup>(6)</sup> |
| 한 번에 자산과 연결 된 고유한 [스트리밍 로케이터](streaming-locators-concept.md) | 100<sup>(7)</sup>(고정) |

<sup>6</sup> 사용자 지정 [스트리밍 정책](/rest/api/media/streamingpolicies)을 사용하는 경우 Media Service 계정에 대해 이러한 정책을 제한적으로 설계하고 동일한 암호화 옵션 및 프로토콜이 필요할 때마다 스트리밍 로케이터에 다시 사용해야 합니다. 각 스트리밍 로케이터에 대해 새 스트리밍 정책을 만들지 않아야 합니다.

<sup>7</sup> 스트리밍 로케이터는 사용자별 액세스 제어를 관리하도록 설계되지 않았습니다. 개별 사용자에게 서로 다른 액세스 권한을 부여하려면 DRM(Digital Rights Management)솔루션을 사용 합니다.

## <a name="protection-limits"></a>보호 제한

| 리소스 | 기본 제한 |
| --- | --- |
| [콘텐츠 키 정책](content-key-policy-concept.md) 당 옵션 |30 |
| 계정당 Media Services 키 전달 서비스의 각 DRM 유형에 대한 월별 라이선스|1,000,000|

## <a name="support-ticket"></a>지원 티켓

고정되지 않는 리소스의 경우 [지원 티켓](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)을 열어 발생되는 할당량을 요청할 수 있습니다. 원하는 할당량 변경, 사용 사례 시나리오 및 필요한 영역에 대한 세부 정보를 요청에 포함시킵니다. <br/>더 높은 한도를 얻기 위해 추가 Azure Media Services 계정을 만들지 **마십시오**.

## <a name="next-steps"></a>다음 단계

[개요](media-services-overview.md)

---
title: 정책 .NET에서 서명 키 가져오기
description: 이 항목에서는 Media Services v3 .NET SDK를 사용하여 기존 정책에서 서명 키를 가져오는 방법을 보여 줍니다.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: how-to
ms.date: 08/31/2020
ms.author: inhenkel
ms.custom: seodec18
ms.openlocfilehash: 1436561f7c82446038c231fadec3bd62c94d4ff9
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98955108"
---
# <a name="get-a-signing-key-from-the-existing-policy"></a>기존 정책에서 서명 키 가져오기

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

v3 API의 핵심 디자인 원칙 중 하나는 API를 더 안전하게 만드는 것입니다. v3 Api는 **가져오기** 또는 **나열** 작업에 대 한 암호 또는 자격 증명을 반환 하지 않습니다. 자세한 내용은 여기를 참조 하세요. 자세한 내용은 [AZURE RBAC 및 Media Services 계정](rbac-overview.md) 을 참조 하세요.

이 문서의 예제에서는 .NET을 사용하여 기존 정책에서 서명 키를 가져오는 방법을 보여 줍니다. 
 
## <a name="download"></a>다운로드 

다음 명령을 사용하여 전체 .NET 샘플이 포함된 GitHub 리포지토리를 컴퓨터에 복제합니다.  

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git
 ```
 
비밀이 있는 ContentKeyPolicy 예제는 [EncryptWithDRM](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/master/AMSV3Tutorials/EncryptWithDRM) 폴더에 있습니다.

## <a name="get-contentkeypolicy-with-secrets"></a>비밀이 있는 ContentKeyPolicy 가져오기 

키로 이동하려면 아래 예제와 같이 **GetPolicyPropertiesWithSecretsAsync** 를 사용합니다.

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/EncryptWithDRM/Program.cs#GetOrCreateContentKeyPolicy)]

## <a name="next-steps"></a>다음 단계

[액세스 제어가 포함된 다중 DRM 콘텐츠 보호 시스템 설계](design-multi-drm-system-with-access-control.md) 

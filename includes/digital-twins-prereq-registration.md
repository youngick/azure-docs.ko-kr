---
author: baanders
description: Azure Digital Twins에 대한 파일 포함 - 앱 등록을 설정하기 위한 필수 구성 요소
ms.service: digital-twins
ms.topic: include
ms.date: 10/29/2020
ms.author: baanders
ms.openlocfilehash: 2ce534972cf6509cdc1ca026f4b29efd3df91afd
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96303591"
---
이 문서에 사용 된 모든 리소스를 인증 하려면 **[Azure Active Directory (Azure AD)](../articles/active-directory/fundamentals/active-directory-whatis.md) 앱 등록을 설정** 해야 합니다. [*방법: 앱 등록 만들기*](../articles/digital-twins/how-to-create-app-registration.md)의 지침에 따라 설정합니다. 

앱 등록이 있으면 등록의 **_애플리케이션(클라이언트) ID_** 및 **_디렉터리(테넌트) ID_**([Azure Portal에서 찾기](../articles/digital-twins/how-to-create-app-registration.md#collect-client-id-and-tenant-id))가 필요합니다. 나중에 Azure Digital Twins API에 액세스 권한을 부여하는 데 사용할 수 있도록 이러한 값을 기록해 둡니다.
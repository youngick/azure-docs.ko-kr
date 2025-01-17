---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/24/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: e9202752d4a33f41cb55d6a0d63a63a3a9baf464
ms.sourcegitcommit: bb330af42e70e8419996d3cba4acff49d398b399
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105031949"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |효과 |버전<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Azure Cache for Redis는 공용 네트워크 액세스를 사용하지 않도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F470baccb-7e51-4549-8b1a-3e5be069f663) |공용 네트워크 액세스를 사용하지 않도록 설정하면 Azure Cache for Redis가 공용 인터넷에 노출되지 않도록 하여 보안이 향상됩니다. 대신 프라이빗 엔드포인트를 만들어 Azure Cache for Redis 노출을 제한할 수 있습니다. [https://docs.microsoft.com/azure/azure-cache-for-redis/cache-private-link](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-private-link)에서 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cache/RedisCache_PublicNetworkAccess_AuditDeny.json) |
|[Azure Cache for Redis는 가상 네트워크 내에 있어야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d092e0a-7acd-40d2-a975-dca21cae48c4) |Azure Virtual Network 배포는 Azure Cache for Redis 외에도 서브넷, 액세스 제어 정책 및 기타 기능에 대한 향상된 보안 및 격리를 제공하여 액세스를 추가로 제한합니다. Azure Cache for Redis 인스턴스가 가상 네트워크를 사용하여 구성되면 주소를 공개적으로 지정할 수 없으며 가상 네트워크 내의 가상 머신 및 애플리케이션에서만 액세스할 수 있습니다. |감사, 거부, 사용 안 함 |[1.0.3](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cache/RedisCache_CacheInVnet_Audit.json) |
|[Azure Cache for Redis는 프라이빗 링크를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7803067c-7d34-46e3-8c79-0ca68fc4036d) |프라이빗 엔드포인트를 사용하면 원본 또는 대상의 공용 IP 주소가 없어도 Azure 서비스에 가상 네트워크를 연결할 수 있습니다. 프라이빗 엔드포인트를 Azure Cache for Redis 인스턴스에 매핑하면 데이터 누출 위험이 줄어듭니다. [https://docs.microsoft.com/azure/azure-cache-for-redis/cache-private-link](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-private-link)에서 자세히 알아보세요. |AuditIfNotExists, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cache/RedisCache_PrivateEndpoint_AuditIfNotExists.json) |
|[공용 네트워크 액세스를 사용하지 않도록 Azure Cache for Redis 구성](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F30b3dfa5-a70d-4c8e-bed6-0083858f663d) |공용 인터넷을 통해 액세스할 수 없도록 Azure Cache for Redis 리소스에 대한 공용 네트워크 액세스를 사용하지 않도록 설정합니다. 이렇게 하면 데이터 유출 위험으로부터 캐시를 보호할 수 있습니다. |수정, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cache/RedisCache_PublicNetworkAccess_Modify.json) |
|[Azure Cache for Redis에 보안 연결만 사용하도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F22bee202-a82f-4305-9a2a-6d7f44d4dedb) |SSL을 통해 설정된 Azure Cache for Redis 연결만 감사 보안 연결을 사용하여 서버와 서비스 간 인증을 보장하고 전송 중인 데이터를 메시지 가로채기(man-in-the-middle), 도청 및 세션 하이재킹과 같은 네트워크 계층 공격으로부터 보호합니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cache/RedisCache_AuditSSLPort_Audit.json) |

---
title: PowerShell 샘플 - 정책이 적용된 모든 애플리케이션 프록시 앱 나열
description: 사용자 디렉터리에서 수명 토큰 정책이 적용된 모든 Azure AD(Azure Active Directory) 애플리케이션 프록시 애플리케이션을 나열하는 PowerShell 예제입니다.
services: active-directory
author: kenwith
manager: daveba
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: sample
ms.date: 12/05/2019
ms.author: kenwith
ms.reviewer: japere
ms.openlocfilehash: c2da1885d975ea6b4daf26714e430143dd89da42
ms.sourcegitcommit: dae6b628a8d57540263a1f2f1cdb10721ed1470d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2021
ms.locfileid: "105709772"
---
# <a name="get-all-application-proxy-apps-with-a-token-lifetime-policy"></a>토큰 수명 정책을 사용하여 모든 애플리케이션 프록시 앱 가져오기

이 PowerShell 스크립트 예제에서는 사용자 디렉터리에서 토큰 수명 정책이 적용된 모든 Azure AD(Azure Active Directory) 애플리케이션 프록시 애플리케이션과 정책 세부 정보를 나열합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [updated-for-az](../../../../includes/updated-for-az.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

이 샘플을 사용하려면 [Graph용 AzureAD V2 PowerShell 모듈 미리 보기 버전](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0-preview&preserve-view=true)(AzureADPreview)이 필요합니다.

## <a name="sample-script"></a>샘플 스크립트

[!code-azurepowershell[main](~/powershell_scripts/application-proxy/get-all-appproxy-apps-with-policy.ps1 "Get all Application Proxy apps with a token lifetime policy")]

## <a name="script-explanation"></a>스크립트 설명

| 명령 | 메모 |
|---|---|
|[Get-AzureADServicePrincipal](/powershell/module/azuread/get-azureadserviceprincipal) | 서비스 주체를 가져옵니다. |
|[Get-AzureADApplication](/powershell/module/azuread/get-azureadapplication) | Azure AD 애플리케이션을 가져옵니다. |
|[Get-AzureADPolicy](/powershell/module/azuread/get-azureadpolicy?view=azureadps-2.0-preview&preserve-view=true) | Azure AD의 정책을 가져옵니다. |
|[Get-AzureADServicePrincipalPolicy](/powershell/module/azuread/get-azureadserviceprincipalpolicy?view=azureadps-2.0-preview&preserve-view=true) | Azure AD의 서비스 주체 정책을 가져옵니다. |


## <a name="next-steps"></a>다음 단계

Azure AD PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 모듈 개요](/powershell/azure/active-directory/overview)를 참조하세요.

애플리케이션 프록시에 대한 다른 PowerShell 예제는 [Azure AD 애플리케이션 프록시에 대한 Azure AD PowerShell 예제](../application-proxy-powershell-samples.md)를 참조하세요.

---
title: 회사 회사 계정 및 파트너 센터
description: 회사에 Microsoft와의 회사 계정이 설정 되어 있는지 확인 하는 방법, 새 회사 계정을 만들거나 파트너 센터에서 사용할 여러 회사 계정을 설정 하는 방법입니다.
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
author: parthpandyaMSFT
ms.author: parthp
ms.date: 05/30/2019
ms.openlocfilehash: 5b4aadc506b2f4a251ccef5e9488066b609ba5a5
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "93130530"
---
# <a name="company-work-accounts-and-partner-center"></a>회사 회사 계정 및 파트너 센터

파트너 센터는 회사 회사 계정 (AD (Azure Active Directory) 테 넌 트 라고도 함)을 사용 하 여 여러 사용자에 대 한 계정 액세스, 제어 권한, 호스트 그룹 및 응용 프로그램을 관리 하 고 프로필 데이터를 유지 관리 합니다. 회사 직원은 회사의 회사 메일 계정 도메인을 파트너 센터 계정에 연결 함으로써 파트너 센터에 로그인 하 여 자신의 회사 계정 사용자 이름 및 암호를 사용 하 여 marketplace 제품을 관리할 수 있습니다.

## <a name="check-whether-your-company-already-has-a-work-account"></a>회사에 회사 계정이 이미 있는지 확인

회사에서 Azure, Microsoft Intune 또는 Microsoft 365와 같은 Microsoft 클라우드 서비스를 구독 한 경우 파트너 센터에서 사용할 수 있는 회사 메일 계정 도메인 (Azure Active Directory 테 넌 트 라고도 함)이 이미 있는 것입니다.

다음 단계를 수행 하 여 확인 합니다.
1. 에서 Azure 관리 포털에 로그인 https://portal.azure.com 합니다.
2. 왼쪽 탐색 메뉴에서 **Azure Active Directory** 를 선택 하 고 **사용자 지정 도메인 이름** 을 선택 합니다.
3. 이미 회사 계정이 있는 경우 도메인 이름이 나열됩니다.

회사에 회사 계정이 아직 없는 경우 파트너 센터 등록 프로세스 중에 사용자에 대 한 계정이 생성 됩니다.

## <a name="set-up-multiple-work-accounts"></a>여러 회사 계정 설정

기존 회사 계정을 사용 하도록 결정 하기 전에 파트너 센터에 액세스 하는 데 필요한 회사 계정 사용자 수를 고려 합니다. 파트너 센터에 액세스할 필요가 없는 회사 계정에 사용자가 있는 경우 파트너 센터에 액세스 해야 하는 사용자만 특정 계정에 표시 되도록 여러 회사 계정을 만드는 것이 좋습니다.

## <a name="create-a-new-work-account"></a>새 회사 계정 만들기

회사에 대 한 새 회사 계정을 만들려면 다음 단계를 수행 합니다. 회사의 Microsoft Azure 계정에 대 한 관리 권한이 있는 사용자에 게 지원을 요청 해야 할 수 있습니다.

1. [Microsoft Azure 포털](https://portal.azure.com)에 로그인합니다.
2. 왼쪽 탐색 메뉴에서 **Azure Active Directory**  ->  **사용자** 를 선택 합니다.
3. **새 사용자** 를 선택 하 고 이름 및 전자 메일 주소를 입력 하 여 새 Azure 회사 계정을 만듭니다. **디렉터리 역할이** **사용자** 로 설정 되어 있는지 확인 하 고 맨 아래에 있는 **암호 표시** 확인란을 선택 하 여 자동 생성 된 암호를 확인 하 고 기록 합니다.
4. **만들기** 를 선택 하 여 새 사용자를 저장 합니다.

사용자 계정에 대 한 전자 메일 주소는 디렉터리에서 확인 된 도메인 이름 이어야 합니다.   ->  왼쪽 탐색 메뉴에서 **사용자 지정 도메인 이름** Azure Active Directory 선택 하 여 디렉터리에 확인 된 도메인을 모두 나열할 수 있습니다.

Azure Active Directory에서 사용자 지정 도메인을 추가 하는 방법에 대해 자세히 알아보려면 [AZURE AD에서 도메인 추가 또는 연결](../../active-directory/fundamentals/add-custom-domain.md)을 참조 하세요.

## <a name="troubleshoot-work-email-sign-in"></a>작업 전자 메일 로그인 문제 해결

회사 계정 (Azure AD 테 넌 트 라고도 함)에 로그인 하는 데 문제가 있는 경우 아래 다이어그램에서 해당 상황과 가장 일치 하는 시나리오를 찾아 권장 단계를 따릅니다.

![작업 계정 로그인 문제 해결을 위한 다이어그램](./media/onboarding-aad-flow.png)

## <a name="next-steps"></a>다음 단계

- [파트너 센터에서 상업용 Marketplace 계정 관리](./manage-account.md)
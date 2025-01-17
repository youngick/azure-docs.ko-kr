---
title: 그룹 멤버 추가 또는 제거 - Azure Active Directory | Microsoft Docs
description: Azure Active Directory를 사용하여 그룹에서 멤버를 추가하거나 제거하는 방법을 알아봅니다.
services: active-directory
author: ajburnle
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: fundamentals
ms.topic: how-to
ms.date: 08/23/2018
ms.author: ajburnle
ms.custom: it-pro, seodec18
ms.reviewer: krbain
ms.collection: M365-identity-device-management
ms.openlocfilehash: af5a85bad1e7b2a6bf645084d6b78f77e6c0d8b2
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92371837"
---
# <a name="add-or-remove-group-members-using-azure-active-directory"></a>Azure Active Directory를 사용하여 그룹 멤버 추가 또는 제거
Azure Active Directory를 사용하여 그룹 멤버를 계속 추가하거나 제거할 수 있습니다.

## <a name="to-add-group-members"></a>그룹 멤버를 추가하려면

1. 디렉터리에 대한 글로벌 관리자 계정을 사용하여 [Azure Portal](https://portal.azure.com)에 로그인합니다.

2. **Azure Active Directory** 를 선택한 다음, **그룹** 을 선택합니다.

3. **그룹 - 모든 그룹** 페이지에서 멤버를 추가할 그룹을 검색하여 선택합니다. 이 경우에 이전에 만든 그룹인 **MDM 정책 - 서부** 를 사용합니다.

    ![그룹 - 그룹 이름이 강조 표시된 모든 그룹 페이지](media/active-directory-groups-members-azure-portal/group-all-groups-screen.png)

4. **MDM 정책 - 서부 개요** 페이지의 **관리** 영역에서 **멤버** 를 선택합니다.

    ![멤버 옵션이 강조 표시된 MDM 정책 - 서부 개요 페이지](media/active-directory-groups-members-azure-portal/group-overview-blade.png)

5. **멤버 추가** 를 선택하고, 그룹에 추가할 멤버를 각각 검색하고 선택한 다음, **선택** 을 선택합니다.

    멤버를 성공적으로 추가했다는 메시지가 표시됩니다.

    ![멤버에 대한 검색이 표시된 멤버 추가 페이지](media/active-directory-groups-members-azure-portal/update-members.png)

6. 그룹에 추가된 모든 멤버 이름을 보려면 화면을 새로 고칩니다.

## <a name="to-remove-group-members"></a>그룹 멤버를 제거하려면

1. **그룹 - 모든 그룹** 페이지에서 멤버를 제거할 그룹을 검색하여 선택합니다. 다시 **MDM 정책 - 서부** 를 사용합니다.

2. **관리** 영역에서 **멤버** 를 선택하고, 제거할 멤버의 이름을 검색하여 선택한 다음, **제거** 를 선택합니다.

    ![제거 옵션을 포함한 멤버 정보 페이지](media/active-directory-groups-members-azure-portal/remove-members-from-group.png)

## <a name="next-steps"></a>다음 단계

- [그룹 및 멤버 보기](active-directory-groups-view-azure-portal.md)

- [그룹 설정 편집](active-directory-groups-settings-azure-portal.md)

- [그룹을 사용하여 리소스에 대한 액세스 관리](active-directory-manage-groups.md)

- [그룹의 사용자에 대한 동적 규칙 관리](../enterprise-users/groups-create-rule.md)

- [Azure Active Directory에 Azure 구독 연결 또는 추가](active-directory-how-subscriptions-associated-directory.md)

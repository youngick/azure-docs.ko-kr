---
title: 빠른 시작 - Azure Portal을 사용하여 감사 보고서 다운로드 | Microsoft Docs
description: Azure Portal을 사용하여 감사 보고서를 다운로드하는 방법 알아보기
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: 4de121ea-f4aa-4c8a-aae4-700c2c5e97a2
ms.service: active-directory
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: report-monitor
ms.date: 11/13/2018
ms.author: markvi
ms.reviewer: dhanyahk
ms.collection: M365-identity-device-management
ms.openlocfilehash: a6cbea49fe39c92c8a2fc50e501cb4ef5cff74b1
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "68989687"
---
# <a name="quickstart-download-an-audit-report-using-the-azure-portal"></a>빠른 시작: Azure Portal을 사용하여 감사 보고서 다운로드

이 빠른 시작에서는 지난 24시간 동안 테넌트에 대한 감사 로그 CSV 파일을 다운로드하는 방법을 알아봅니다. Azure Portal에서 최대 250,000개의 레코드를 다운로드할 수 있습니다. 레코드는 가장 최근 순으로 정렬되므로 기본적으로 가장 최근의 250,000개 레코드를 가져옵니다. 

## <a name="prerequisites"></a>필수 구성 요소

다음 작업을 수행해야 합니다.

* Azure Active Directory 테넌트. 
* 테넌트에 대한 **보안 관리자**, **보안 읽기 권한자** 또는 **글로벌 관리자** 역할의 사용자 또한 테넌트의 모든 사용자는 자신의 감사 로그에 액세스할 수 있습니다.

## <a name="quickstart-download-an-audit-report"></a>빠른 시작: 감사 보고서 다운로드

1. [Azure Portal](https://portal.azure.com)로 이동합니다.
2. 왼쪽 탐색 창에서 **Azure Active Directory** 를 선택하고 **디렉터리 전환** 단추를 사용하여 Active Directory를 선택합니다.
3. 대시보드에서 **Azure Active Directory** 를 선택한 다음, **감사 로그** 를 선택합니다. 
4. **날짜 범위** 필터 드롭다운에서 **지난 24시간** 을 선택하고 **적용** 을 선택하여 지난 24시간 동안의 감사 로그를 확인합니다. 
5. **다운로드** 단추를 선택하고 파일 형식으로 **CSV** 를 선택한 후 필터링된 레코드가 포함된 CSV 파일을 다운로드할 파일 이름을 지정합니다. 

![보고](./media/quickstart-download-audit-report/download-audit-logs.png)

## <a name="next-steps"></a>다음 단계

* [Azure Active Directory 포털의 로그인 활동 보고서](concept-sign-ins.md)
* [Azure Active Directory Reporting 보존](reference-reports-data-retention.md)
* [Azure Active Directory 보고 대기 시간](reference-reports-latencies.md)

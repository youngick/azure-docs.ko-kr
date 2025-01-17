---
title: Azure 빠른 시작 - Azure Automation 계정 만들기 | Microsoft Docs
description: 이 문서는 Azure Automation 계정을 만들고 Runbook을 실행하는 데 도움이 됩니다.
services: automation
ms.date: 04/04/2019
ms.topic: quickstart
ms.subservice: process-automation
ms.custom: mvc
ms.openlocfilehash: a07c6ac524aa213519ace1ae204ac2d76db802aa
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "83836705"
---
# <a name="create-an-azure-automation-account"></a>Azure Automation 계정 만들기

여러 리소스에 대한 액세스를 허용하는 브라우저 기반 사용자 인터페이스인 Azure Portal을 사용하여 Azure를 통해 Azure Automation 계정을 만들 수 있습니다. 하나의 Automation 계정으로 해당 테넌트의 모든 영역과 구독 전반의 리소스를 관리할 수 있습니다. 

이 빠른 시작에서는 Automation 계정을 만들고 계정에서 Runbook을 실행하는 방법을 안내합니다. Azure 구독이 아직 없는 경우 시작하기 전에 [Azure 체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.

## <a name="sign-in-to-azure"></a>Azure에 로그인

[Azure에 로그인](https://portal.azure.com)합니다.

## <a name="create-automation-account"></a>Automation 계정 만들기

1. Azure 계정의 이름을 선택합니다. Automation 계정 이름은 하위 지역 및 리소스 그룹별로 고유합니다. 삭제된 Automation 계정의 이름은 즉시 사용할 수 없습니다.

    > [!NOTE]
    > 사용자 인터페이스에 입력된 계정 이름은 변경할 수 없습니다. 

2. Azure Portal의 왼쪽 위 모서리에 있는 **리소스 만들기** 단추를 클릭합니다.

3. **IT 및 관리 도구** 를 선택한 다음, **Automation** 을 선택합니다.

4. 선택한 계정 이름을 포함한 계정 정보를 입력합니다. Azure에 대한 인증을 간소화하는 아티팩트를 자동으로 사용하도록 설정하기 위해 **Azure 실행 계정 만들기** 에서 **예** 를 선택합니다. 정보 입력이 완료되면 **만들기** 를 클릭하여 Automation 계정 배포를 시작합니다.

    ![페이지에서 Automation 계정에 대한 정보 입력](./media/automation-quickstart-create-account/create-automation-account-portal-blade.png)  

    > [!NOTE]
    > Automation 계정을 배포할 수 있는 위치의 업데이트된 목록은 [지역별로 사용 가능한 제품](https://azure.microsoft.com/global-infrastructure/services/?products=automation&regions=all)을 참조하세요.

5. 배포가 완료되면 **모든 서비스** 를 클릭합니다.

6. **Automation 계정** 을 선택한 다음, 사용자가 만든 Automation 계정을 선택합니다.

    ![Automation 계정 개요](./media/automation-quickstart-create-account/automation-account-overview.png)

## <a name="run-a-runbook"></a>Runbook 실행

자습서 Runbook 중 하나를 실행합니다.

1. **프로세스 자동화** 아래에서 **Runbook** 을 클릭합니다. Runbook 목록이 표시됩니다. 기본적으로 몇 가지 자습서 Runbook을 계정에서 사용할 수 있습니다.

    ![Automation 계정 Runbook 목록](./media/automation-quickstart-create-account/automation-runbooks-overview.png)

1. **AzureAutomationTutorialScript** Runbook을 선택합니다. Runbook 개요 페이지가 열립니다.

    ![Runbook 개요](./media/automation-quickstart-create-account/automation-tutorial-script-runbook-overview.png)

1. **시작** 을 클릭하고 Runbook 시작 페이지에서 **확인** 을 클릭하여 Runbook을 시작합니다.

    ![Runbook 작업 페이지](./media/automation-quickstart-create-account/automation-tutorial-script-job.png)

1. 작업 상태가 `Running`이 되면 **출력** 또는 **모든 로그** 를 클릭하여 Runbook 작업 출력을 확인합니다. 이 자습서 Runbook의 경우 출력은 Azure 리소스 목록입니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 Automation 계정을 배포하고, Runbook 작업을 시작하고, 작업 결과를 확인했습니다. Azure Automation에 대한 자세한 내용을 알아보려면 첫 번째 Runbook을 만드는 빠른 시작으로 계속 진행하세요.

> [!div class="nextstepaction"]
> [Automation 빠른 시작 - Azure Automation Runbook 만들기](./automation-quickstart-create-runbook.md)


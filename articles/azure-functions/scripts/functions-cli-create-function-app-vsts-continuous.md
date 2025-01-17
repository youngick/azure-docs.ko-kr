---
title: DevOps 배포를 사용하여 함수 앱 만들기 - Azure CLI
description: 함수 앱 만들기 및 Azure DevOps의 함수 코드 배포
ms.date: 07/03/2018
ms.topic: sample
ms.custom: mvc, devx-track-azurecli
ms.openlocfilehash: f89da9fc146d753442f2a8c8aa38861e66c9a3d9
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97934379"
---
# <a name="create-a-function-in-azure-that-is-deployed-from-azure-devops"></a>Azure에서 Azure DevOps로부터 배포되는 함수 만들기

이 항목에서는 Azure Functions를 사용하여 [소비 계획](../consumption-plan.md)을 사용하는 [서버리스](https://azure.microsoft.com/solutions/serverless/) 함수 앱을 만드는 방법을 보여 줍니다. 함수의 컨테이너에 해당하는 함수 앱은 Azure DevOps 리포지토리에서 지속적으로 배포됩니다. 

이 항목을 완료하려면 다음 항목이 필요합니다.

* 함수 앱 프로젝트를 포함하고 사용자에게 관리 권한이 있는 Azure DevOps 리포지토리
* Azure DevOps 리포지토리에 액세스하기 위한 [PAT(개인용 액세스 토큰)](/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](../../../includes/azure-cli-prepare-your-environment.md)]

 - 이 자습서에는 Azure CLI 버전 2.0 이상이 필요합니다. Azure Cloud Shell을 사용하는 경우 최신 버전이 이미 설치되어 있습니다. 

## <a name="sample-script"></a>샘플 스크립트

이 샘플은 Azure 함수 앱을 만들고 Azure DevOps의 함수 코드를 배포합니다.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용하여 리소스 그룹, 스토리지 계정, 함수 앱 및 모든 관련된 리소스를 만듭니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az storage account create](/cli/azure/storage/account#az-storage-account-create) | 함수 앱에 필요한 스토리지 계정을 만듭니다. |
| [az functionapp create](/cli/azure/functionapp#az-functionapp-create) | 서버리스 [소비 계획](../consumption-plan.md)에서 함수 앱을 만듭니다. |
| [az functionapp deployment source config](/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config) | Git 또는 Mercurial 리포지토리를 사용하여 함수 앱에 연결합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure)를 참조하세요.

추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.

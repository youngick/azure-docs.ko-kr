---
title: Azure Resource Manager 템플릿 샘플 - Event Grid | Microsoft Docs
description: 이 문서에서는 GitHub의 Azure Event Grid에 대한 Azure Resource Manager 템플릿 샘플 목록을 제공합니다.
ms.topic: sample
ms.date: 07/07/2020
ms.openlocfilehash: 910012adf2dc930e6f1a26f1a7fc41f5ed0580c9
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "86119058"
---
# <a name="azure-resource-manager-templates-for-event-grid"></a>Event Grid를 위한 Azure Resource Manager 템플릿

템플릿에서 사용할 JSON 구문 및 속성은 [Microsoft.EventGrid 리소스 종류](/azure/templates/microsoft.eventgrid/allversions)를 참조하세요. 다음 표는 Event Grid를 위한 Azure Resource Manager 템플릿 링크를 포함합니다.

## <a name="event-grid-subscriptions"></a>Event Grid 구독
- [웹후크 엔드포인트를 통한 사용자 지정 항목 및 구독](https://github.com/Azure/azure-quickstart-templates/tree/master/101-event-grid) - Event Grid 사용자 지정 항목을 배포합니다. 웹후크 엔드포인트를 사용하여 해당 사용자 지정 항목에 대한 구독을 만듭니다. 
- [EventHub 엔드포인트를 통한 사용자 지정 항목 구독](https://github.com/Azure/azure-quickstart-templates/tree/master/101-event-grid-event-hubs-handler) - 사용자 지정 항목에 대한 Event Grid 구독을 만듭니다. 구독은 엔드포인트에 대해 Event Hub를 사용합니다. 
- [Azure 구독 또는 리소스 그룹 구독](https://github.com/Azure/azure-quickstart-templates/tree/master/101-event-grid-resource-events-to-webhook) - 리소스 그룹 또는 Azure 구독에 대한 이벤트를 구독합니다. 배포 중 대상으로 지정하는 리소스 그룹은 이벤트의 원본입니다. 구독은 엔드포인트에 웹후크를 사용합니다. 
- [Blob 스토리지 계정 및 구독](https://github.com/Azure/azure-quickstart-templates/tree/master/101-event-grid-subscription-and-storage) - Azure Blob Storage 계정을 배포하고 해당 스토리지 계정에 대한 이벤트를 구독합니다. 

## <a name="next-steps"></a>다음 단계
다음 샘플을 참조하세요.

- [PowerShell 샘플](powershell-samples.md)
- [CLI 샘플](cli-samples.md)

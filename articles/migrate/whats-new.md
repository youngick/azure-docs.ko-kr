---
title: Azure Migrate의 새로운 기능
description: Azure Migrate 서비스의 새로운 기능 및 최신 업데이트에 대해 알아봅니다.
ms.topic: overview
author: anvar-ms
ms.author: anvar
ms.manager: bsiva
ms.date: 04/19/2020
ms.custom: mvc
ms.openlocfilehash: 41476c5f8165729caa6780f8e74eb6c3ae30a59c
ms.sourcegitcommit: d135e9a267fe26fbb5be98d2b5fd4327d355fe97
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/10/2021
ms.locfileid: "102614635"
---
# <a name="whats-new-in-azure-migrate"></a>Azure Migrate의 새로운 기능

[Azure Migrate](migrate-services-overview.md)를 사용하면 온-프레미스 서버, 앱 및 데이터를 검색 및 평가하고 Microsoft Azure 클라우드로 마이그레이션할 수 있습니다. 이 문서에서는 Azure Migrate의 새로운 릴리스와 기능이 요약되어 있습니다.

## <a name="update-march-2021"></a>업데이트(2021년 3월)
- Azure Migrate 어플라이언스에서 여러 서버 자격 증명을 제공하여 설치된 애플리케이션(소프트웨어 인벤토리), 에이전트 없는 종속성 분석을 검색하고 VMware 환경에서 SQL Server 인스턴스와 데이터베이스를 검색할 수 있도록 지원합니다. [자세한 정보](tutorial-discover-vmware.md#provide-server-credentials)
- VMware 환경에서 실행되는 SQL Server 인스턴스 및 데이터베이스를 검색하고 평가하는 기능은 현재 미리 보기로 제공됩니다. [자세한 내용](concepts-azure-sql-assessment-calculation.md)<br/>이 기능을 사용해 보려면 [이 링크](https://aka.ms/AzureMigrate/SQL)를 통해 **오스트레일리아 동부** 지역의 프로젝트를 만드세요. 시작하려면 [검색](tutorial-discover-vmware.md) 및 [평가](tutorial-assess-sql.md) 자습서를 참조하세요.
- 에이전트 없는 VMware 마이그레이션은 이제 vCenter당 500개의 VM 동시 복제를 지원합니다.
- 이제 Azure Migrate는 에이전트 없는 VMware 마이그레이션 메서드를 사용하여 Azure로 마이그레이션하는 동안 VMware VM에 Azure VM 에이전트를 자동으로 설치합니다.

## <a name="update-january-2021"></a>업데이트(2021년 1월)
-  Azure Migrate: 이제 서버 마이그레이션 도구를 사용하면 CMK(고객 관리형 키)를 통해 서버 쪽 암호화로 암호화된 디스크를 사용하여 VMware 가상 머신, 물리적 서버 및 가상 머신을 다른 클라우드에서 Azure 가상 머신으로 마이그레이션할 수 있습니다.

## <a name="update-december-2020"></a>업데이트(2020년 12월)
- 이제 Azure Migrate는 에이전트 없는 VMware 마이그레이션 메서드를 사용하여 Azure로 마이그레이션하는 동안 VMware VM에 Azure VM 에이전트를 자동으로 설치합니다.
- 이제 Azure Portal을 통해 사용 가능한 Azure Migrate 서버 마이그레이션(에이전트 없는 복제)을 사용하여 CMK(고객 관리형 키)에서 SSE(서버 쪽 암호화)를 사용하여 암호화된 디스크로 VMware VM을 Azure 가상 머신으로 마이그레이션할 수 있습니다.

## <a name="update-september-2020"></a>업데이트(2020년 9월)
- 이제 가용성 영역으로의 서버 마이그레이션이 지원됩니다.
- 이제 UEFI 기반 VM 및 물리적 서버를 Azure 2세대 VM으로 마이그레이션할 수 있습니다. 이 릴리스를 통해 Azure Migrate: 서버 마이그레이션 도구는 마이그레이션 중에 Gen 2 VM에서 Gen 1 VM으로의 변환을 수행하지 않습니다.
- 새로운 Azure Migrate Power BI 평가 대시보드를 사용하여 다양한 평가 설정에서 비용을 비교할 수 있습니다. 대시보드는 Power BI 대시보드에 연결되는 평가를 자동으로 만드는 PowerShell 유틸리티와 함께 제공됩니다. [자세한 정보](https://github.com/Azure/azure-docs-powershell-samples/tree/master/azure-migrate/assessment-utility)
- 이제 1000개의 VM에서 종속성 분석(에이전트 없는)을 동시에 실행할 수 있습니다.
- 이제 PowerShell 스크립트를 사용하여 종속성 분석(에이전트 없는)을 대규모로 활성화하거나 비활성화할 수 있습니다. [자세한 정보](https://github.com/Azure/azure-docs-powershell-samples/tree/master/azure-migrate/dependencies-at-scale)
- 종속성 분석(에이전트 없음)을 통해 수집된 데이터를 사용하여 Power BI에서 네트워크 연결을 시각화합니다. [자세히 알아보세요.](https://github.com/Azure/azure-docs-powershell-samples/tree/master/azure-migrate/dependencies-at-scale)
- 이제 Azure Migrate를 사용하여 데이터 디스크 크기가 최대 32TB인 VMware VM 마이그레이션이 지원됩니다. 서버 마이그레이션 에이전트 없는 VMware 마이그레이션 메서드.

## <a name="update-august-2020"></a>업데이트(2020년 8월)

- 포털에서 Azure Migrate 프로젝트 키가 생성되고 어플라이언스 등록을 완료하는 데 사용되는 온보딩 환경이 개선되었습니다.
- 포털에서 OVA/VHD 파일 또는 설치 관리자 스크립트를 다운로드하여 각각 VMware 및 Hyper-V 어플라이언스를 설정하는 옵션입니다.
- 향상된 사용자 환경으로 어플라이언스 구성 관리자를 새로 고쳤습니다.
- Hyper-V VM 검색을 위한 여러 자격 증명 지원.

## <a name="update-july-2020"></a>업데이트(2020년 7월)

- 에이전트 없는 VMware 마이그레이션은 이제 vCenter당 300개의 VM 동시 복제를 지원합니다.

## <a name="update-june-2020"></a>업데이트(2020년 6월)

- 이제 온-프레미스 VMware VM을 [AVS(Azure VMware 솔루션)](./concepts-azure-vmware-solution-assessment-calculation.md)로 마이그레이션하기 위한 평가가 지원됩니다. [자세히 알아보기](how-to-create-azure-vmware-solution-assessment.md)
- 물리적 서버 검색에 대한 어플라이언스의 여러 자격 증명을 지원합니다.
- 테넌트 제한이 구성된 테넌트에 대해 어플라이언스에서 Azure 로그인을 허용하도록 지원합니다.


## <a name="update-april-2020"></a>업데이트(2020년 4월)

Azure Migrate는 Azure Government에서의 배포를 지원합니다. 

- VMware VM, Hyper-V VM 및 물리적 서버를 검색 및 평가할 수 있습니다.
- VMware VM, Hyper-V VM 및 물리적 서버를 Azure로 마이그레이션할 수 있습니다.
- VMware 마이그레이션의 경우 에이전트 없는 또는 에이전트 기반 마이그레이션을 사용할 수 있습니다. [자세히 알아보기](server-migrate-overview.md).
- Azure Government에 대해 지원되는 지역 및 영역을 [검토](migrate-support-matrix.md#supported-geographies-azure-government)합니다.
- [에이전트 기반 종속성 분석](concepts-dependency-visualization.md#agent-based-analysis)은 Azure Government에서 지원되지 않습니다.
- 미리 보기의 기능은 Azure Government, 특히 [에이전트 없는 종속성 분석](concepts-dependency-visualization.md#agentless-analysis), [애플리케이션 검색](how-to-discover-applications.md)에서 지원됩니다.


## <a name="update-march-2020"></a>업데이트(2020년 3월)

이제 [Azure Migrate 어플라이언스](migrate-appliance.md)를 설정하는 스크립트 기반 설치를 사용할 수 있습니다.

- 스크립트 기반 설치는 어플라이언스의 .OVA(VMware)/VHD(Hyper-V) 설치의 대안입니다.
- Windows Server 2016을 실행하는 기존 머신에서 VMware/Hyper-V용 어플라이언스를 설정하는 데 사용할 수 있는 PowerShell 설치 관리자 스크립트를 제공합니다.

## <a name="update-november-2019"></a>업데이트(2019년 11월)

Azure Migrate에 여러 가지 새로운 기능이 추가되었습니다.

- **물리적 서버 평가**. 이미 지원되는 물리적 서버 마이그레이션 외에도 온-프레미스 물리적 서버의 평가가 지원됩니다.
- **가져오기 기반 평가**. 이제 CSV 파일로 제공되는 메타데이터 및 성능 데이터를 사용한 컴퓨터 평가가 지원됩니다.
- **애플리케이션 검색**: Azure Migrate는 이제 Azure Migrate 어플라이언스를 사용하여 애플리케이션 수준의 앱, 역할 및 기능 검색을 지원합니다. 이는 현재 VMware VM에서만 지원되며 검색으로만 제한됩니다(평가는 현재 지원되지 않음). [자세히 알아보기](how-to-discover-applications.md)
- **에이전트 없는 종속성 시각화**: 종속성 시각화를 위해 더 이상 에이전트를 명시적으로 설치할 필요가 없습니다. 이제 에이전트 없이 또는 에이전트 기반이 모두 지원됩니다.
- **가상 데스크톱**: ISV 도구를 사용하여 온-프레미스 VDI(가상 데스크톱 인프라)를 평가하고 Azure의 Windows Virtual Desktop으로 마이그레이션합니다.
- **웹앱**: 이제 웹앱을 평가하고 마이그레이션하는 데 사용되는 Azure App Service Migration Assistant가 Azure Migrate에 통합되었습니다.

Azure Migrate에 새로운 평가 및 마이그레이션 도구가 추가되었습니다.

- **RackWare**: 제품 클라우드 마이그레이션.
- **Movere**: 제품 평가.

Azure Migrate에서 평가 및 마이그레이션을 위해 도구 및 ISV 제품을 사용하는 방법에 대해 [자세히 알아봅니다](migrate-services-overview.md).

## <a name="azure-migrate-current-version"></a>Azure Migrate 현재 버전

현재 버전의 Azure Migrate(2019년 7월 릴리스됨)는 다음과 같은 여러 가지 새로운 기능을 제공합니다.

- **통합 마이그레이션 플랫폼**: 이제 Azure Migrate는 향상된 배포 흐름과 포털 환경을 통해 Azure에 대한 마이그레이션 과정을 중앙에서 처리하고, 관리 및 추적하는 단일 포털을 제공합니다.
- **평가 및 마이그레이션 도구**: Azure Migrate는 기본 도구를 제공하고, ISV(독립 소프트웨어 공급업체) 도구 뿐만 아니라 다른 Azure 서비스와 연결됩니다. ISV 통합에 대해 [자세히 알아보세요](migrate-services-overview.md#isv-integration).
- **Azure Migrate 평가**: Azure Migrate Server 평가 도구를 사용하여 Azure로의 마이그레이션에 대해 VMware VM 및 Hyper-V VM을 평가할 수 있습니다. 또한 다른 Azure 서비스 및 ISV 도구를 사용하여 마이그레이션을 평가할 수도 있습니다.
- **Azure Migrate 마이그레이션**: Azure Migrate 서버 마이그레이션 도구를 사용하여 온-프레미스 VMware VM 및 Hyper-V VM을 실제 서버, 다른 가상화된 서버, 프라이빗/퍼블릭 클라우드 VM 뿐만 아니라 Azure로 마이그레이션할 수 있습니다. 또한 ISV 도구를 사용하여 Azure로 마이그레이션할 수 있습니다.
- **Azure Migrate 어플라이언스**: Azure Migrate는 온-프레미스 VMware VM 및 Hyper-V VM의 검색 및 평가를 위해 경량 어플라이언스를 배포합니다.
    - 이 어플라이언스는 Azure Migrate 서버 평가에 사용되고, 에이전트 없는 마이그레이션을 위해 Azure Migrate 서버 마이그레이션에서 사용됩니다.
    - 어플라이언스는 평가 및 마이그레이션을 위해 서버 메타데이터 및 성능 데이터를 지속적으로 검색합니다.  
- **VMware VM 마이그레이션**:  Azure Migrate 서버 마이그레이션은 온-프레미스 VMware VM을 Azure로 마이그레이션하기 위한 몇 가지 방법을 제공합니다.  Azure Migrate 어플라이언스를 사용하는 에이전트 없는 마이그레이션과 복제 어플라이언스를 사용하며 마이그레이션하려는 각 VM에 에이전트를 배포하는 에이전트 기반 마이그레이션이 있습니다. [자세히 알아보기](server-migrate-overview.md)
 - **데이터베이스 평가 및 마이그레이션**: Azure Migrate에서 Azure Database Migration Assistant를 사용하여 Azure로 마이그레이션하기 위한 온-프레미스 데이터베이스를 평가할 수 있습니다. Azure Database Migration Service를 사용하여 데이터베이스를 마이그레이션할 수 있습니다.
- **웹앱 마이그레이션**: Azure App Service와 함께 퍼블릭 엔드포인트 URL을 사용하여 웹앱을 평가할 수 있습니다. 내부 .NET 앱의 마이그레이션을 위해 App Service Migration Assistant를 다운로드하여 실행할 수 있습니다.
- **Data Box**: Azure Migrate에서 Azure Data Box를 사용하여 많은 양의 오프라인 데이터를 Azure로 가져옵니다.

## <a name="azure-migrate-previous-version"></a>Azure Migrate 이전 버전

이전 버전의 Azure Migrate를 사용하고 있었다면(온-프레미스 VMware VM의 평가만 지원됨) 이제 현재 버전을 사용해야 합니다. 이전 버전에서는 더 이상 새 Azure Migrate 프로젝트를 만들거나 새 검색을 수행할 수 없습니다. 기존 프로젝트에 계속 액세스할 수 있습니다. Azure Portal > **모든 서비스** 에서 이 작업을 수행하려면 **Azure Migrate** 를 검색합니다. Azure Migrate 알림에는 이전 Azure Migrate 프로젝트에 액세스할 수 있는 링크가 있습니다.



## <a name="next-steps"></a>다음 단계

- Azure Migrate 가격 책정에 대해 [자세히 알아봅니다](https://azure.microsoft.com/pricing/details/azure-migrate/).
- Azure Migrate에 대한 [질문과 대답을 검토합니다](resources-faq.md).
- [VMware VM](./tutorial-assess-vmware-azure-vm.md) 및 [Hyper-V VM](tutorial-assess-hyper-v.md)을 평가하는 자습서를 사용해 보세요.
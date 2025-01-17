---
title: Azure에서 Service Fabric 런타임 업그레이드
description: 이 자습서에서는 PowerShell을 사용하여 Azure 호스팅 Service Fabric 클러스터의 런타임을 업그레이드하는 방법을 알아봅니다.
ms.topic: tutorial
ms.date: 07/22/2019
ms.custom: mvc
ms.openlocfilehash: 23b3aabf8e991e512ef9a5c07d725c3084ea7f83
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "86244738"
---
# <a name="tutorial-upgrade-the-runtime-of-a-service-fabric-cluster-in-azure"></a>자습서: Azure에서 Service Fabric 클러스터의 런타임 업그레이드

이 자습서는 시리즈의 4부로, Azure Service Fabric 클러스터에서 Service Fabric 런타임을 업그레이드하는 방법을 보여 줍니다. 이 자습서 편은 Azure에서 실행되는 Service Fabric 클러스터를 대상으로 하며 독립 실행형 Service Fabric 클러스터에는 해당하지 않습니다.

> [!WARNING]
> 이 자습서 편에는 PowerShell이 필요합니다. Azure CLI 도구에서는 클러스터 런타임 업그레이드가 아직 지원되지 않습니다. 대신 포털에서 클러스터를 업그레이드할 수 있습니다. 자세한 내용은 [Azure Service Fabric 클러스터 업그레이드](service-fabric-cluster-upgrade.md)를 참조하세요.

클러스터가 이미 최신 Service Fabric 런타임을 실행 중이라면 이 단계가 필요하지 않습니다. 그러나 이 문서를 사용하여 Azure Service Fabric 클러스터에 지원되는 런타임을 설치할 수 있습니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
> * 클러스터 버전 읽기
> * 클러스터 버전 설정

이 자습서 시리즈에서는 다음 방법에 대해 알아봅니다.
> [!div class="checklist"]
> * 템플릿을 사용하여 Azure에서 보안 [Windows 클러스터](service-fabric-tutorial-create-vnet-and-windows-cluster.md) 만들기
> * [클러스터 모니터링](service-fabric-tutorial-monitor-cluster.md)
> * [클러스터 규모 확장 또는 규모 감축](service-fabric-tutorial-scale-cluster.md)
> * 클러스터의 런타임 업그레이드
> * [클러스터 삭제](service-fabric-tutorial-delete-cluster.md)


[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="prerequisites"></a>필수 구성 요소

이 자습서를 시작하기 전에:

* Azure 구독이 없는 경우 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.
* [Azure PowerShell](/powershell/azure/install-az-ps) 또는 [Azure CLI](/cli/azure/install-azure-cli)를 설치합니다.
* Azure에서 보안 [Windows 클러스터](service-fabric-tutorial-create-vnet-and-windows-cluster.md) 만들기
* Windows 개발 환경을 설정합니다. [Visual Studio 2019](https://www.visualstudio.com), **Azure 개발**, **ASP.NET 및 웹 개발** 및 **.NET Core 플랫폼 간 개발** 워크로드를 설치합니다.  그런 후 [.NET 개발 환경](service-fabric-get-started.md)을 설정합니다.

### <a name="sign-in-to-azure"></a>Azure에 로그인

Azure 명령을 실행하기 전에 Azure 계정에 로그인하고 구독을 선택합니다.

```powershell
Connect-AzAccount
Get-AzSubscription
Set-AzContext -SubscriptionId <guid>
```

## <a name="get-the-runtime-version"></a>런타임 버전 가져오기

Azure에 연결하고 Service Fabric 클러스터가 포함된 구독을 선택했으면 클러스터의 런타임 버전을 가져올 수 있습니다.

```powershell
Get-AzServiceFabricCluster -ResourceGroupName SFCLUSTERTUTORIALGROUP -Name aztestcluster `
    | Select-Object ClusterCodeVersion
```

또는 다음 예제를 통해 구독의 모든 클러스터 목록을 가져옵니다.

```powershell
Get-AzServiceFabricCluster | Select-Object Name, ClusterCodeVersion
```

**ClusterCodeVersion** 값을 확인합니다. 이 값은 다음 섹션에서 사용됩니다.

## <a name="upgrade-the-runtime"></a>런타임 업그레이드

`Get-ServiceFabricRuntimeUpgradeVersion` cmdlet과 이전 섹션의 **ClusterCodeVersion** 값을 사용하여 업그레이드할 수 있는 버전을 확인합니다. 이 cmdlet은 인터넷에 연결된 컴퓨터에서만 실행할 수 있습니다. 예를 들어, `5.7.198.9494` 버전에서 업그레이드할 수 있는 런타임 버전을 확인하려면 다음 명령을 사용합니다.

```powershell
Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion "5.7.198.9494"
```

버전 목록에서 Azure Service Fabric 클러스터에 더 나중인 런타임으로 업그레이드하도록 지시할 수 있습니다. 예를 들어 `6.0.219.9494` 버전으로 업그레이드할 수 있으면 다음 명령을 사용하여 클러스터를 업그레이드합니다.

```powershell
Set-AzServiceFabricUpgradeType -ResourceGroupName SFCLUSTERTUTORIALGROUP `
                                    -Name aztestcluster `
                                    -UpgradeMode Manual `
                                    -Version "6.0.219.9494"
```

> [!IMPORTANT]
> 클러스터 런타임 업그레이드를 완료하는 데 다소 시간이 걸릴 수 있습니다. 업그레이드 중에는 PowerShell이 차단됩니다. 다른 PowerShell 세션을 사용하여 업그레이드 상태를 확인할 수 있습니다.

업그레이드 상태는 PowerShell이나 Azure Service Fabric CLI(sfctl)로 모니터링할 수 있습니다.

먼저 클러스터를 자습서의 첫 부분에서 만든 TLS/SSL 인증서에 연결합니다. `Connect-ServiceFabricCluster` cmdlet 또는 `sfctl cluster upgrade-status`를 사용합니다.

```powershell
$endpoint = "<mycluster>.southcentralus.cloudapp.azure.com:19000"
$thumbprint = "63EB5BA4BC2A3BADC42CA6F93D6F45E5AD98A1E4"

Connect-ServiceFabricCluster -ConnectionEndpoint $endpoint `
                             -KeepAliveIntervalInSec 10 `
                             -X509Credential -ServerCertThumbprint $thumbprint `
                             -FindType FindByThumbprint -FindValue $thumbprint `
                             -StoreLocation CurrentUser -StoreName My
```

```console
sfctl cluster select --endpoint https://aztestcluster.southcentralus.cloudapp.azure.com:19080 \
--pem ./aztestcluster201709151446.pem --no-verify
```

다음으로 `Get-ServiceFabricClusterUpgrade` 또는 `sfctl cluster upgrade-status`를 사용하여 상태를 표시합니다. 결과는 다음 응답과 유사합니다.

```powershell
Get-ServiceFabricClusterUpgrade

TargetCodeVersion                          : 6.0.219.9494
TargetConfigVersion                        : 3
StartTimestampUtc                          : 11/28/2017 3:09:48 AM
UpgradeState                               : RollingForwardPending
UpgradeDuration                            : 00:09:00
CurrentUpgradeDomainDuration               : 00:09:00
NextUpgradeDomain                          : 1
UpgradeDomainsStatus                       : { "0" = "Completed";
                                             "1" = "Pending";
                                             "2" = "Pending";
                                             "3" = "Pending";
                                             "4" = "Pending" }
UpgradeKind                                : Rolling
RollingUpgradeMode                         : Monitored
FailureAction                              : Rollback
ForceRestart                               : False
UpgradeReplicaSetCheckTimeout              : 37201.09:59:01
HealthCheckWaitDuration                    : 00:05:00
HealthCheckStableDuration                  : 00:05:00
HealthCheckRetryTimeout                    : 00:45:00
UpgradeDomainTimeout                       : 02:00:00
UpgradeTimeout                             : 12:00:00
ConsiderWarningAsError                     : False
MaxPercentUnhealthyApplications            : 0
MaxPercentUnhealthyNodes                   : 100
ApplicationTypeHealthPolicyMap             : {}
EnableDeltaHealthEvaluation                : True
MaxPercentDeltaUnhealthyNodes              : 0
MaxPercentUpgradeDomainDeltaUnhealthyNodes : 0
ApplicationHealthPolicyMap                 : {}
```

```console
sfctl cluster upgrade-status

{
  "codeVersion": "6.0.219.9494",
  "configVersion": "3",

... item cut to save space ...

  },
  "upgradeDomains": [
    {
      "name": "0",
      "state": "Completed"
    },
    {
      "name": "1",
      "state": "Pending"
    },
    {
      "name": "2",
      "state": "Pending"
    },
    {
      "name": "3",
      "state": "Pending"
    },
    {
      "name": "4",
      "state": "Pending"
    }
  ],
  "upgradeDurationInMilliseconds": "PT1H2M4.63889S",
  "upgradeState": "RollingForwardPending"
}
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.

> [!div class="checklist"]
> * 클러스터 런타임 버전 가져오기
> * 클러스터 런타임 업그레이드
> * 업그레이드 모니터링

다음 자습서를 진행합니다.

> [!div class="nextstepaction"]
> [클러스터 삭제](service-fabric-tutorial-delete-cluster.md)

---
title: 자습서 - Azure Red Hat OpenShift 4 클러스터 만들기
description: Azure CLI를 사용하여 Microsoft Azure Red Hat OpenShift 클러스터를 만드는 방법 알아보기
author: sakthi-vetrivel
ms.author: suvetriv
ms.topic: tutorial
ms.service: azure-redhat-openshift
ms.date: 10/26/2020
ms.openlocfilehash: 55c1b6f6c6690f0c8f00a8a2469834781f35fb3c
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102449801"
---
# <a name="tutorial-create-an-azure-red-hat-openshift-4-cluster"></a>자습서: Azure Red Hat OpenShift 4 클러스터 만들기

총 3부 중 1부에 해당하는 이 자습서에서는 OpenShift 4를 실행하는 Azure Red Hat OpenShift 클러스터를 만들 환경을 준비한 후 클러스터를 만들겠습니다. 이 문서에서 배울 내용은 다음과 같습니다.
> [!div class="checklist"]
> * 필수 구성 요소 설정 
> * 필요한 가상 네트워크 및 서브넷 만들기
> * 클러스터 배포

## <a name="before-you-begin"></a>시작하기 전에

CLI를 로컬로 설치하여 사용하도록 선택하는 경우 이 자습서에서는 Azure CLI 버전 2.6.0 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요.

Azure Red Hat OpenShift에는 OpenShift 클러스터를 만들고 실행하는 데 최소 40개의 코어가 필요합니다. 새 Azure 구독에 대한 기본 Azure 리소스 할당량은 이 요구 사항을 충족하지 않습니다. 리소스 제한 늘리기를 요청하려면 [표준 할당량: VM 시리즈별 제한 늘리기](../azure-portal/supportability/per-vm-quota-requests.md)를 참조하세요.

ARO 끌어오기 비밀은 ARO에 대한 RH OpenShift 라이선스의 비용을 변경하지 않습니다.

### <a name="verify-your-permissions"></a>권한 확인

이 자습서를 진행하는 동안 클러스터의 가상 네트워크를 포함하는 리소스 그룹을 만듭니다. 가상 네트워크에 직접 연결하거나 가상 네트워크를 포함하는 리소스 그룹 또는 구독에 대한 기여자 및 사용자 액세스 관리자 권한 또는 소유자 권한이 있어야 합니다.

또한 클러스터를 대신하여 애플리케이션 및 서비스 주체를 만들 수 있는 도구에 충분한 Azure Active Directory 권한이 필요합니다.

### <a name="register-the-resource-providers"></a>리소스 공급자 등록

1. 여러 Azure 구독이 있는 경우 관련 구독 ID를 지정합니다.

    ```azurecli-interactive
    az account set --subscription <SUBSCRIPTION ID>
    ```

1. `Microsoft.RedHatOpenShift` 리소스 공급자를 등록합니다.

    ```azurecli-interactive
    az provider register -n Microsoft.RedHatOpenShift --wait
    ```
    
1. `Microsoft.Compute` 리소스 공급자를 등록합니다.

    ```azurecli-interactive
    az provider register -n Microsoft.Compute --wait
    ```
    
1. `Microsoft.Storage` 리소스 공급자를 등록합니다.

    ```azurecli-interactive
    az provider register -n Microsoft.Storage --wait
    ```
    
1. `Microsoft.Authorization` 리소스 공급자를 등록합니다.

    ```azurecli-interactive
    az provider register -n Microsoft.Authorization --wait
    ```

### <a name="get-a-red-hat-pull-secret-optional"></a>Red Hat 풀 비밀 가져오기(선택 사항)

Red Hat 풀 비밀을 사용하면 클러스터에서 추가 콘텐츠와 함께 Red Hat 컨테이너 레지스트리에 액세스할 수 있습니다. 이 단계는 선택 사항이지만 권장됩니다.

1. [Red Hat OpenShift 클러스터 매니저 포털로 이동](https://cloud.redhat.com/openshift/install/azure/aro-provisioned)하여 로그인합니다.

   회사 이메일로 Red Hat 계정에 로그인하거나 새 Red Hat 계정을 만들고 사용 약관에 동의해야 합니다.

1. **풀 비밀 다운로드** 를 클릭하고 ARO 클러스터에서 사용할 풀 비밀을 다운로드합니다.

    저장된 `pull-secret.txt` 파일을 안전한 위치에 보관합니다. Red Hat 또는 인증된 파트너에 대한 샘플 또는 연산자를 포함하는 클러스터를 만들어야 하는 경우 각 클러스터 만들기에 파일이 사용됩니다.

    `az aro create` 명령을 실행하는 경우 `--pull-secret @pull-secret.txt` 매개 변수를 사용하여 풀 비밀을 참조할 수 있습니다. `pull-secret.txt` 파일을 저장한 디렉터리에서 `az aro create`를 실행합니다. 그렇지 않으면 `@pull-secret.txt`를 `@/path/to/my/pull-secret.txt`로 바꿉니다.

    풀 비밀을 복사하거나 다른 스크립트에서 참조하는 경우에는 풀 비밀을 유효한 JSON 문자열로 포맷해야 합니다.

### <a name="prepare-a-custom-domain-for-your-cluster-optional"></a>클러스터에 대한 사용자 지정 도메인 준비(선택 사항)

`az aro create` 명령을 실행할 때 `--domain foo.example.com` 매개 변수를 사용하여 클러스터의 사용자 지정 도메인을 지정할 수 있습니다.

클러스터에 사용자 지정 도메인을 제공하는 경우 다음 사항에 유의하세요.

* 클러스터를 만든 후 지정된 `--domain`에 대해 DNS 서버에 2개의 DNS A 레코드를 만들어야 합니다.
    * **api** - api 서버 IP 주소를 가리킵니다.
    * **\*.apps** - 수신 IP 주소를 가리킵니다.
    * 클러스터 생성 후 `az aro show -n -g --query '{api:apiserverProfile.ip, ingress:ingressProfiles[0].ip}'` 명령을 실행하여 이러한 값을 검색합니다.

* OpenShift 콘솔은 기본 제공 도메인 `https://console-openshift-console.apps.<random>.<location>.aroapp.io` 대신 `https://console-openshift-console.apps.example.com`과 같은 URL에서 사용할 수 있습니다.

* 기본적으로 OpenShift는 사용자 지정 도메인 `*.apps.example.com`에서 만든 모든 경로에 자체 서명된 인증서를 사용합니다.  클러스터에 연결한 후 사용자 지정 DNS를 사용하도록 선택하면 OpenShift 설명서에 따라 [수신 컨트롤러의 사용자 지정 CA](https://docs.openshift.com/container-platform/4.6/security/certificates/replacing-default-ingress-certificate.html) 및 [API 서버의 사용자 지정 CA](https://docs.openshift.com/container-platform/4.6/security/certificates/api-server.html)를 구성해야 합니다.

### <a name="create-a-virtual-network-containing-two-empty-subnets"></a>두 개의 빈 서브넷이 있는 가상 네트워크 만들기

다음으로, 두 개의 빈 서브넷이 있는 가상 네트워크를 만들겠습니다. 요구 사항을 충족하는 기존 가상 네트워크가 있는 경우 이 단계를 건너뛸 수 있습니다.

1. **`az` 명령을 실행하는 셸 환경에서 다음 변수를 설정합니다.**

   ```console
   LOCATION=eastus                 # the location of your cluster
   RESOURCEGROUP=aro-rg            # the name of the resource group where you want to create your cluster
   CLUSTER=cluster                 # the name of your cluster
   ```

2. **리소스 그룹을 만듭니다.**

   Azure 리소스 그룹은 Azure 리소스가 배포되고 관리되는 논리 그룹입니다. 리소스 그룹을 만들 때 위치를 지정하라는 메시지가 나타납니다. 이 위치는 리소스 그룹 메타데이터가 저장되는 위치이며 리소스를 만드는 동안 다른 지역을 지정하지 않으면 리소스가 Azure에서 실행되는 위치이기도 합니다. [az group create](/cli/azure/group#az-group-create) 명령을 사용하여 리소스 그룹을 만듭니다.
    
   > [!NOTE] 
   > Azure 리소스 그룹을 만들 수 있는 일부 지역에서는 Azure Red Hat OpenShift를 사용할 수 없습니다. Azure Red Hat OpenShift가 지원되는 위치에 대한 정보는 [사용 가능한 지역](https://azure.microsoft.com/en-gb/global-infrastructure/services/?products=openshift)을 참조하세요.

   ```azurecli-interactive
   az group create \
     --name $RESOURCEGROUP \
     --location $LOCATION
   ```

   다음 예제 출력에서는 성공적으로 만들어진 리소스 그룹이 나와 있습니다.

   ```json
   {
     "id": "/subscriptions/<guid>/resourceGroups/aro-rg",
     "location": "eastus",
     "name": "aro-rg",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "type": "Microsoft.Resources/resourceGroups"
   }
   ```

2. **가상 네트워크를 만듭니다.**

   OpenShift 4를 실행하는 Azure Red Hat OpenShift 클러스터에는 마스터 및 작업자 노드에 사용할 두 개의 빈 서브넷이 있는 가상 네트워크가 필요합니다. 이를 위해 새 가상 네트워크를 만들거나 기존 가상 네트워크를 사용할 수 있습니다.

   이전에 만든 동일한 리소스 그룹에 새 가상 네트워크를 만듭니다.

   ```azurecli-interactive
   az network vnet create \
      --resource-group $RESOURCEGROUP \
      --name aro-vnet \
      --address-prefixes 10.0.0.0/22
   ```

   다음 예제 출력을 보면 가상 네트워크가 성공적으로 만들어졌습니다.

   ```json
   {
     "newVNet": {
       "addressSpace": {
         "addressPrefixes": [
           "10.0.0.0/22"
         ]
       },
       "dhcpOptions": {
         "dnsServers": []
       },
       "id": "/subscriptions/<guid>/resourceGroups/aro-rg/providers/Microsoft.Network/virtualNetworks/aro-vnet",
       "location": "eastus",
       "name": "aro-vnet",
       "provisioningState": "Succeeded",
       "resourceGroup": "aro-rg",
       "type": "Microsoft.Network/virtualNetworks"
     }
   }
   ```

3. **마스터 노드에 사용할 빈 서브넷을 추가합니다.**

   ```azurecli-interactive
   az network vnet subnet create \
     --resource-group $RESOURCEGROUP \
     --vnet-name aro-vnet \
     --name master-subnet \
     --address-prefixes 10.0.0.0/23 \
     --service-endpoints Microsoft.ContainerRegistry
   ```

4. **작업자 노드에 사용할 빈 서브넷을 추가합니다.**

   ```azurecli-interactive
   az network vnet subnet create \
     --resource-group $RESOURCEGROUP \
     --vnet-name aro-vnet \
     --name worker-subnet \
     --address-prefixes 10.0.2.0/23 \
     --service-endpoints Microsoft.ContainerRegistry
   ```

5. **마스터 서브넷에서 [서브넷 프라이빗 엔드포인트 정책을 사용하지 않도록 설정](../private-link/disable-private-link-service-network-policy.md)합니다.** 이는 서비스가 클러스터에 연결하고 관리하는 데 필요합니다.

   ```azurecli-interactive
   az network vnet subnet update \
     --name master-subnet \
     --resource-group $RESOURCEGROUP \
     --vnet-name aro-vnet \
     --disable-private-link-service-network-policies true
   ```

## <a name="create-the-cluster"></a>클러스터 만들기

다음 명령을 실행하여 클러스터를 만듭니다. 다음 옵션 중 하나를 사용하도록 선택하는 경우 이에 따라 명령을 수정합니다.
* 필요에 따라 [Red Hat 풀 비밀을 전달](#get-a-red-hat-pull-secret-optional)할 수 있습니다. 그러면 클러스터에서 추가 콘텐츠와 함께 Red Hat 컨테이너 레지스트리에 액세스할 수 있습니다. 명령에 `--pull-secret @pull-secret.txt` 인수를 추가합니다.
* 필요에 따라 [사용자 지정 도메인을 사용](#prepare-a-custom-domain-for-your-cluster-optional)할 수 있습니다. `foo.example.com`을 사용자 지정 도메인으로 대체하는 `--domain foo.example.com` 인수를 명령에 추가합니다.

> [!NOTE]
> 명령에 선택적 인수를 추가하는 경우 뒤에 백슬래시를 사용하여 명령의 이전 줄에서 인수를 닫아야 합니다.

```azurecli-interactive
az aro create \
  --resource-group $RESOURCEGROUP \
  --name $CLUSTER \
  --vnet aro-vnet \
  --master-subnet master-subnet \
  --worker-subnet worker-subnet
```

`az aro create` 명령을 실행한 후 클러스터를 만드는 데 일반적으로 약 35분이 소요됩니다.

## <a name="next-steps"></a>다음 단계

자습서의 이 부분에서는 다음 방법에 대해 알아봅니다.
> [!div class="checklist"]
> * 필수 구성 요소를 설정하고 필요한 가상 네트워크 및 서브넷 만들기
> * 클러스터 배포

다음 자습서를 진행합니다.
> [!div class="nextstepaction"]
> [Azure Red Hat OpenShift 클러스터에 연결](tutorial-connect-cluster.md)

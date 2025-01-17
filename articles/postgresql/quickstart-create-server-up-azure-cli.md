---
title: '빠른 시작: 서버 만들기 - az postgres up - Azure Database for PostgreSQL - 단일 서버'
description: Azure CLI(명령줄 인터페이스) up 명령을 사용하여 Azure Database for PostgreSQL - 단일 서버를 만들기 위한 빠른 시작 가이드입니다.
author: lfittl-msft
ms.author: lufittl
ms.service: postgresql
ms.devlang: azurecli
ms.topic: quickstart
ms.date: 05/06/2019
ms.custom: devx-track-azurecli
ms.openlocfilehash: c11a98c04f81e7c111faf4aa449ab2bf9a4890bb
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92485225"
---
# <a name="quickstart-use-an-azure-cli-command-az-postgres-up-preview-to-create-an-azure-database-for-postgresql---single-server"></a>빠른 시작: Azure CLI 명령인 az postgres up(미리 보기)을 사용하여 Azure Database for PostgreSQL - 단일 서버 만들기

> [!IMPORTANT]
> [az postgres up](/cli/azure/ext/db-up/postgres#ext-db-up-az-postgres-up) Azure CLI 명령은 미리 보기에 있습니다.

PostgreSQL용 Azure Database는 클라우드에서 항상 사용 가능한 PostgreSQL 데이터베이스를 실행, 관리 및 크기 조정할 수 있게 하는 관리 서비스입니다. 명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure CLI가 사용됩니다. 이 빠른 시작에서는 Azure CLI에서 [az postgres up](/cli/azure/ext/db-up/postgres#ext-db-up-az-postgres-up) 명령을 사용하여 Azure Database for PostgreSQL 서버를 만드는 방법을 보여줍니다. `az postgres up` 명령은 서버를 만드는 것 외에도 샘플 데이터베이스(데이터베이스에 루트 사용자)를 만들고, Azure 서비스에 대한 방화벽을 열고, 클라이언트 컴퓨터에 대한 기본 방화벽 규칙을 만듭니다. 이러한 기본값은 개발 프로세스를 빠르게 진행하는 데 도움이 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

이 문서에서는 Azure CLI 버전 2.0 이상을 로컬로 실행해야 합니다. 설치된 버전을 확인하려면 `az --version` 명령을 실행합니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요.

[az login](/cli/azure/authenticate-azure-cli) 명령을 사용하여 계정에 로그인해야 합니다. 해당 구독 이름에 대한 명령 출력에서 **ID** 속성을 참고합니다.

```azurecli
az login
```

구독이 여러 개인 경우 리소스가 과금되어야 할 적절한 구독을 선택합니다. [az account set](/cli/azure/account) 명령을 사용하여 계정에 속한 특정 구독 ID를 선택합니다. 구독에 대한 **az login** 출력의 **구독 ID** 속성을 구독 ID 자리 표시자로 바꿉니다.

```azurecli
az account set --subscription <subscription id>
```

## <a name="create-an-azure-database-for-postgresql-server"></a>PostgreSQL용 Azure Database 서버 만들기

명령을 사용하려면 [db-up](/cli/azure/ext/db-up) 확장을 설치합니다. 오류가 반환되면 최신 버전의 Azure CLI를 설치했는지 확인합니다. [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요.

```azurecli
az extension add --name db-up
```

다음 명령을 사용하여 Azure Database for PostgreSQL 서버를 만듭니다.

```azurecli
az postgres up
```

수동으로 재정의하지 않는 한 서버는 다음과 같은 기본값으로 만들어집니다.

**설정** | **기본값** | **설명**
---|---|---
서버 이름 | 시스템 생성 | PostgreSQL 서버용 Azure Database를 식별하는 고유한 이름입니다.
resource-group | 시스템 생성 | 새 Azure 리소스 그룹입니다.
sku-name | GP_Gen5_2 | SKU의 이름입니다. {가격 책정 계층}\_{계산 세대}\_{vCores} 규칙을 축약형으로 따릅니다. 기본값은 2개의 vCore가 있는 범용 5세대 서버입니다. 계층에 대한 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/postgresql/)를 참조하세요.
backup-retention | 7 | 장기 백업이 보존되는 방법입니다. 단위는 일입니다.
geo-redundant-backup | 사용 안 함 | 이 서버에 지역 중복 백업을 사용할 것인지 여부를 결정합니다.
위치 | westus2 | 서버에 대한 Azure 위치입니다.
ssl-enforcement | 사용 안 함 | 이 서버에 TLS/SSL을 사용할 것인지 여부를 결정합니다.
storage-size | 5120 | 서버의 스토리지 용량입니다(단위는 메가바이트).
버전 | 10 | PostgreSQL 주 버전입니다.
admin-user | 시스템 생성 | 관리자의 사용자 이름입니다.
admin-password | 시스템 생성 | 관리자 사용자의 암호입니다.

> [!NOTE]
> `az postgres up` 명령과 해당 추가 매개 변수에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/ext/db-up/postgres#ext-db-up-az-postgres-up)를 참조하세요.

서버가 만들어지면 다음과 같은 설정이 제공됩니다.

- “devbox”라는 방화벽 규칙이 만들어집니다. Azure CLI는 `az postgres up` 명령이 실행되는 머신의 IP 주소를 검색하여 해당 IP 주소를 허용합니다.
- “Azure 서비스에 대한 액세스 허용”이 켜기로 설정됩니다. 이 설정은 구독에 없는 리소스를 포함하여 모든 Azure 리소스로부터의 연결을 허용하도록 서버의 방화벽을 구성합니다.
- “sampledb”라는 빈 데이터베이스가 만들어집니다.
- “sampledb”에 대한 권한이 있는 “root”라는 새 사용자가 만들어집니다.

> [!NOTE]
> Azure Databases for PostgreSQL은 5432 포트를 통해 통신합니다. 회사 네트워크 내에서 연결하려는 경우 5432 포트를 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다. 서버에 연결하려면 IT 부서에서 5432 포트를 열도록 요청하세요.

## <a name="get-the-connection-information"></a>연결 정보 가져오기

`az postgres up` 명령이 완료되면 인기 있는 프로그래밍 언어에 대한 연결 문자열 목록이 반환됩니다. 이러한 연결 문자열은 새로 만든 Azure Database for PostgreSQL 서버의 특정 특성으로 미리 구성되어 있습니다.

[az postgres show-connection-string](/cli/azure/ext/db-up/postgres#ext-db-up-az-postgres-show-connection-string) 명령을 사용하여 이러한 연결 문자열을 다시 나열할 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

다음 명령을 사용하여 빠른 시작에서 만든 모든 리소스를 정리합니다. 이 명령은 Azure Database for PostgreSQL 서버 및 리소스 그룹을 삭제합니다.

```azurecli
az postgres down --delete-group
```

새로 만든 서버만 삭제하려면 [az postgres down](/cli/azure/ext/db-up/postgres#ext-db-up-az-postgres-down) 명령을 실행할 수 있습니다.

```azurecli
az postgres down
```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)

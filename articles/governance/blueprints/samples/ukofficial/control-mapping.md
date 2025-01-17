---
title: 영국 공식 및 영국 NHS 청사진 샘플 제어
description: 영국 공식 및 영국 NHS 청사진 샘플의 제어 매핑입니다. 각 컨트롤은 평가를 지원하는 하나 이상의 Azure Policy 정의에 매핑됩니다.
ms.date: 02/05/2021
ms.topic: sample
ms.openlocfilehash: bf10bcf7064306094664c1ff560187ef77645d4d
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99627569"
---
# <a name="control-mapping-of-the-uk-official-and-uk-nhs-blueprint-samples"></a>영국 공식 및 영국 NHS 청사진 샘플의 제어 매핑

이 문서에서는 영국 공식 및 영국 NHS 청사진 샘플이 영국 공식 및 영국 NHS 제어에 매핑되는 방법에 대해 자세히 설명합니다. 제어에 대한 자세한 내용은 [영국 공식](https://www.gov.uk/government/publications/government-security-classifications)을 참조하세요.

다음은 **영국 공식** 및 **UK NHS** 제어에 대한 매핑입니다. 특정 컨트롤 매핑으로 바로 점프하려면 오른쪽의 탐색 기능을 사용합니다. 많은 매핑된 컨트롤은 [Azure Policy](../../../policy/overview.md) 이니셔티브를 사용하여 구현됩니다. 전체 이니셔티브를 검토하려면 Azure Portal에서 **정책** 을 열고 **정의** 페이지를 선택합니다. 그런 다음, **\[미리 보기\] UK OFFICIAL 및 UK NHS 제어 감사 및 감사 요구 사항을 지원하는 특정 VM 확장 배포** 기본 제공 정책 이니셔티브를 찾아서 선택합니다.

> [!IMPORTANT]
> 아래의 각 컨트롤은 하나 이상의 [Azure Policy](../../../policy/overview.md) 정의와 연결되어 있습니다. 이러한 정책은 컨트롤을 사용한 [규정 준수 평가](../../../policy/how-to/get-compliance-data.md)에 도움이 될 수 있지만, 컨트롤과 하나 이상의 정책 간에 일대일 또는 완벽한 일치 관계가 없는 경우도 많습니다. 따라서 Azure Policy의 **규정 준수** 는 정책 자체만 가리킬 뿐, 컨트롤의 모든 요구 사항을 완벽하게 준수한다는 것은 아닙니다. 또한 규정 준수 표준에는 현재 Azure Policy 정의에서 처리되지 않은 컨트롤이 포함되어 있습니다. 따라서 Azure Policy의 규정 준수는 전반적인 규정 준수 상태를 부분적으로 표시할 뿐입니다. 이 규정 준수 청사진 샘플에 대한 컨트롤과 Azure Policy 정의 간의 연결은 시간이 지남에 따라 변경될 수 있습니다. 변경 기록을 보려면 [GitHub 커밋 기록](https://github.com/MicrosoftDocs/azure-docs/commits/master/articles/governance/blueprints/samples/ukofficial/control-mapping.md)을 참조하세요.

## <a name="1-data-in-transit-protection"></a>1 전송 중 데이터 보호

이 청사진은 스토리지 계정 및 Redis Cache에 대한 안전하지 않은 연결을 감사하는 [Azure Policy](../../../policy/overview.md) 정의를 할당하여 Azure 서비스를 사용한 정보 전송이 안전하게 수행되도록 하는 데 도움이 됩니다.

- Redis Cache에 보안 연결만 사용하도록 설정해야 합니다.
- Storage 계정에 보안 전송을 사용하도록 설정해야 합니다.
- 보안 통신 프로토콜을 사용하지 않는 Windows 웹 서버의 감사 결과 표시
- 웹 애플리케이션에 HTTPS를 통해서만 액세스 가능
- 함수 앱에 HTTPS를 통해서만 액세스 가능
- API 앱은 HTTPS를 통해서만 액세스할 수 있어야 합니다.

## <a name="23-data-at-rest-protection"></a>2.3 저장 데이터 보호

이 청사진은 특정 암호화 제어를 적용하고 약한 암호화 설정 사용을 감사하는 [Azure Policy](../../../policy/overview.md) 정의를 할당하여 암호화 제어 사용에 대한 정책을 적용하는 데 도움이 됩니다. Azure 리소스의 암호화 구성이 최적이 아닐 수 있는 경우를 이해하면 리소스가 정보 보안 정책에 따라 구성되도록 정정 작업을 수행하는 데 도움이 될 수 있습니다. 특히, 이 청사진에서 할당하는 정책을 적용하려면 다음 사항을 고려해야 합니다. Data Lake 스토리지 계정에 대한 암호화가 필요합니다. SQL 데이터베이스에서 투명한 암호화가 필요합니다. 스토리지 계정, SQL 데이터베이스, 가상 머신 디스크 및 자동화 계정 변수에서 누락된 암호화를 감사합니다. 스토리지 계정 및 Redis Cache에 대한 안전하지 않은 연결을 감사합니다. 약한 가상 머신 암호 암호화를 감사합니다. 암호화되지 않은 Service Fabric 통신을 감사합니다.

- 가상 머신에서 디스크 암호화를 적용해야 합니다.
- 자동화 계정 변수를 암호화해야 합니다.
- Service Fabric 클러스터의 ClusterProtectionLevel 속성을 EncryptAndSign으로 설정해야 합니다.
- SQL 데이터베이스에 투명한 데이터 암호화를 사용하도록 설정해야 합니다.
- SQL DB 투명한 데이터 암호화 배포
- Data Lake Store 계정에서 암호화 필요
- 허용된 위치("영국 남부" 및 "영국 서부"로 하드 코딩됨)
- 리소스 그룹이 허용된 위치("영국 남부" 및 "영국 서부"로 하드 코딩됨)

## <a name="52-vulnerability-management"></a>5.2 취약성 관리

이 청사진은 누락된 엔드포인트 보호, 누락된 시스템 업데이트, 운영 체제 취약성, SQL 취약성 및 가상 머신 취약성을 모니터링하는 [Azure Policy](../../../policy/overview.md) 정의를 할당하여 정보 시스템 취약성을 관리하는 데 도움이 됩니다. 이러한 인사이트는 배포된 리소스의 보안 상태에 대한 실시간 정보를 제공하며, 업데이트 관리 작업의 우선 순위를 지정하는 데 도움이 될 수 있습니다.

- Azure Security Center에서 누락된 Endpoint Protection 모니터링
- 시스템 업데이트를 머신에 설치해야 합니다.
- 가상 머신 확장 집합에 대한 시스템 업데이트를 설치해야 합니다.
- 머신 보안 구성의 취약성을 수정해야 합니다.
- SQL 데이터베이스의 취약성을 수정해야 합니다.
- 취약성 평가 솔루션으로 취약성을 수정해야 합니다.
- SQL 서버에서 취약성 평가를 사용하도록 설정해야 합니다.
- SQL 관리형 인스턴스에서 취약성 평가를 사용하도록 설정해야 함
- 가상 머신 확장 집합에서 보안 구성의 취약성을 수정해야 합니다.
- SQL 관리형 인스턴스에서 Advanced Data Security를 사용하도록 설정해야 함
- SQL Server에서 Advanced Data Security를 사용하도록 설정해야 합니다.

## <a name="53-protective-monitoring"></a>5.3 보호 모니터링

이 청사진은 무제한 액세스, 목록 활동 허용 및 위협에 대한 보호 모니터링을 제공하는 [Azure Policy](../../../policy/overview.md) 정의를 할당하여 정보 시스템 자산을 보호하는 데 도움이 됩니다.

- 스토리지 계정은 네트워크 액세스를 제한해야 함
- 머신에서 안전한 애플리케이션을 정의하기 위해 적응형 애플리케이션 제어를 사용하도록 설정해야 함
- 재해 복구를 구성하지 않고 가상 머신 감사
- Azure DDoS Protection 표준을 사용하도록 설정해야 함
- SQL 관리형 인스턴스의 Advanced Data Security 설정에서 Advanced Threat Protection 유형을 '모두'로 설정해야 합니다.
- SQL Server의 Advanced Data Security 설정에서 Advanced Threat Protection 유형을 '모두'로 설정해야 합니다.
- SQL 서버에 위협 탐지 배포
- Windows Server용 기본 Microsoft IaaSAntimalware 확장 배포

## <a name="9-secure-user-management"></a>9개 안전한 사용자 관리 

Azure RBAC(Azure 역할 기반 액세스 제어)는 Azure에서 리소스에 액세스할 수 있는 사용자를 관리하는 데 도움이 됩니다.
Azure Portal을 사용하여 Azure 리소스에 대한 액세스 권한이 있는 사용자 및 해당 사용자의 권한을 검토할 수 있습니다. 이 청사진은 소유자 및/또는 읽기/쓰기 권한이 있는 외부 계정과 다단계 인증을 사용하도록 설정되지 않은 소유자, 읽기 및/또는 쓰기 권한이 있는 계정을 감사하는 [Azure Policy](../../../policy/overview.md) 정의를 할당하여 액세스 권한을 제한하고 제어하는 데 도움이 됩니다.

- 구독에서 소유자 권한이 있는 계정에 MFA를 사용하도록 설정해야 합니다.
- 구독에서 쓰기 권한이 있는 계정에 MFA를 사용하도록 설정해야 합니다.
- 구독에서 읽기 권한이 있는 계정에 MFA를 사용하도록 설정해야 합니다.
- 소유자 권한이 있는 외부 계정은 구독에서 제거해야 합니다.
- 쓰기 권한이 있는 외부 계정을 구독에서 제거해야 합니다.
- 읽기 권한이 있는 외부 계정을 구독에서 제거해야 합니다.

## <a name="10-identity-and-authentication"></a>10개 ID 및 인증

이 청사진은 소유자 및/또는 읽기/쓰기 권한이 있는 외부 계정과 다단계 인증을 사용하도록 설정되지 않은 소유자, 읽기 및/또는 쓰기 권한이 있는 계정을 감사하는 [Azure Policy](../../../policy/overview.md) 정의를 할당하여 액세스 권한을 제한하고 제어하는 데 도움이 됩니다.

- 구독에서 소유자 권한이 있는 계정에 MFA를 사용하도록 설정해야 합니다.
- 구독에서 쓰기 권한이 있는 계정에 MFA를 사용하도록 설정해야 합니다.
- 구독에서 읽기 권한이 있는 계정에 MFA를 사용하도록 설정해야 합니다.
- 소유자 권한이 있는 외부 계정은 구독에서 제거해야 합니다.
- 쓰기 권한이 있는 외부 계정을 구독에서 제거해야 합니다.
- 읽기 권한이 있는 외부 계정을 구독에서 제거해야 합니다.

이 청사진은 SQL Server 및 Service Fabric에 대한 Azure Active Directory 인증 사용을 감사하는 Azure Policy 정의를 할당합니다. Azure Active Directory 인증을 사용하면 데이터베이스 사용자 및 기타 Microsoft 서비스의 권한을 간편하게 관리하고 ID를 한 곳에서 집중적으로 관리할 수 있습니다.

- SQL Server에 대해 Azure Active Directory 관리자를 프로비저닝해야 합니다.
- Service Fabric 클러스터는 클라이언트 인증에 대해서만 Azure Active Directory를 사용해야 합니다.

또한 이 청사진은 사용 중단된 계정 및 외부 계정을 포함하여 검토를 위해 우선 순위를 지정해야 하는 계정을 감사하는 Azure Policy 정의를 할당합니다. 필요한 경우 계정을 로그인하지 못하게 차단하거나 제거하여 Azure 리소스에 대한 액세스 권한을 즉시 제거할 수 있습니다.
이 청사진은 제거할 대상으로 고려해야 하는 사용 중단된 계정을 감사하는 두 개의 Azure Policy 정의를 할당합니다.

- 더 이상 사용되지 않는 계정은 구독에서 제거해야 합니다.
- 소유자 권한이 있는 사용되지 않는 계정은 구독에서 제거해야 합니다.
- 소유자 권한이 있는 외부 계정은 구독에서 제거해야 합니다.
- 쓰기 권한이 있는 외부 계정을 구독에서 제거해야 합니다.

또한 이 청사진은 Linux VM 암호 파일 권한을 감사하여 잘못 설정된 경우 경고하는 Azure Policy 정의를 할당합니다. 이 설계를 사용하면 인증자가 손상되지 않도록 정정 작업을 수행할 수 있습니다.

- passwd 파일 권한이 0644로 설정되지 않은 Linux VM의 감사 결과 표시

이 청사진은 최소 강도 및 기타 암호 요구 사항을 적용하지 않는 Windows VM을 감사하는 Azure Policy 정의를 할당하여 강한 암호를 적용하는 데 도움이 됩니다. 암호 강도 정책을 위반하는 VM을 인식하면 모든 VM 사용자 계정의 암호가 정책을 준수하도록 정정 작업을 수행하는 데 도움이 됩니다.

- 암호 복잡성 설정이 사용되지 않는 Windows VM의 감사 결과 표시
- 암호 최대 사용 기간이 70일로 설정되지 않은 Windows VM의 감사 결과 표시
- 암호 최소 사용 기간이 1일로 설정되지 않은 Windows VM의 감사 결과 표시
- 암호 최소 길이가 14자로 제한되지 않는 Windows VM의 감사 결과 표시
- 이전 24개 암호의 재사용을 허용하는 Windows VM의 감사 결과 표시

또한 이 청사진은 Azure Policy 정의를 할당하여 Azure 리소스에 대한 액세스를 제어하는 데 도움이 됩니다. 이 정책은 리소스에 더 많은 권한의 액세스를 허용할 수 있는 리소스 유형의 사용을 감사합니다. 이 정책을 위반하는 리소스를 이해하면 Azure 리소스 액세스가 권한 있는 사용자로 제한되도록 정정 작업을 수행하는 데 도움이 될 수 있습니다.

- 암호 없는 계정이 있는 Linux VM의 감사 결과 표시
- 암호 없이 계정에서 원격으로 연결할 수 있는 Linux VM의 감사 결과를 표시합니다.
- 스토리지 계정을 새 Azure Resource Manager 리소스로 마이그레이션해야 합니다.
- 가상 머신을 새 Azure Resource Manager 리소스로 마이그레이션해야 합니다.
- 관리 디스크를 사용하지 않는 VM 감사

## <a name="11-external-interface-protection"></a>11 외부 인터페이스 보호

이 청사진은 적절한 보안 사용자 관리를 위해 25개가 넘는 정책을 사용하는 것 외에도 무제한 스토리지 계정을 모니터링하는 [Azure 정책](../../../policy/overview.md) 정의를 할당하여 무단 액세스로부터 서비스 인터페이스를 보호하는 데 도움이 됩니다.
무제한 액세스 권한이 있는 스토리지 계정을 사용하면 정보 시스템 내에 포함된 정보에 대한 의도하지 않은 액세스를 허용할 수 있습니다. 또한 이 청사진은 가상 머신에서 적응형 애플리케이션 제어를 사용하도록 설정하는 정책을 할당합니다.

- 스토리지 계정은 네트워크 액세스를 제한해야 함
- 머신에서 안전한 애플리케이션을 정의하기 위해 적응형 애플리케이션 제어를 사용하도록 설정해야 함
- 인터넷 연결 엔드포인트를 통한 액세스를 제한해야 합니다.
- 적응형 네트워크 강화 추천 사항은 인터넷에 연결된 가상 머신에 적용해야 합니다.
- 가상 머신 확장 집합에 Endpoint Protection 솔루션을 설치해야 합니다.
- 가상 머신의 관리 포트는 Just-In-Time 네트워크 액세스 제어로 보호해야 함
- 함수 앱에 대해 원격 디버깅을 해제해야 합니다.
- 웹 애플리케이션에 대해 원격 디버깅을 해제해야 합니다.
- API Apps에 대해 원격 디버깅을 해제해야 합니다.

## <a name="13-audit-information-for-users"></a>13 사용자 정보 감사

이 청사진을 사용하면 Azure 리소스에 대한 로그 설정을 감사하는 [Azure Policy](../../../policy/overview.md) 정의를 할당하여 시스템 이벤트가 기록되도록 할 수 있습니다.
또한 할당된 정책은 가상 머신이 로그를 지정된 로그 분석 작업 영역에 보내지 않는지도 감사합니다.

- SQL Server에서 Advanced Data Security를 사용하도록 설정해야 합니다.
- 진단 설정 감사
- \[미리 보기\]: Linux VM용 Log Analytics 에이전트 배포
- \[미리 보기\]: Windows VM용 Log Analytics 에이전트 배포
- 가상 네트워크를 만들 때 Network Watcher 배포


## <a name="next-steps"></a>다음 단계

이제 영국 공식 및 UK NHS 청사진의 제어 매핑을 살펴보았으므로 다음 문서를 참조하여 이 샘플의 개요 및 이를 배포하는 방법을 알아봅니다.

> [!div class="nextstepaction"]
> [영국 공식 및 영국 NHS 청사진 - 개요](./index.md)
> [영국 공식 및 영국 NHS 청사진 - 배포 단계](./deploy.md)

청사진 및 사용 방법에 대한 추가 문서:

- [청사진 수명 주기](../../concepts/lifecycle.md)에 대해 알아봅니다.
- [정적 및 동적 매개 변수](../../concepts/parameters.md) 사용 방법 이해
- [청사진 시퀀싱 순서](../../concepts/sequencing-order.md)를 사용자 지정하는 방법 알아보기
- [청사진 리소스 잠금](../../concepts/resource-locking.md)을 활용하는 방법 알아보기
- [기존 할당을 업데이트](../../how-to/update-existing-assignments.md)하는 방법 알아보기

---
author: rayne-wiselman
ms.service: site-recovery
ms.topic: include
ms.date: 10/26/2018
ms.author: raynew
ms.openlocfilehash: 8076a6af2382ccec1ac832cd83c3946d8c7c6f57
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96019146"
---
|매개 변수 이름| Type | 설명| 가능한 값|
|-|-|-|-|
| /ServerMode|필수|구성 서버와 프로세스 서버를 모두 설치할지 또는 프로세스 서버만 설치할지 여부를 지정합니다.|CS<br>PS|
|/InstallLocation|필수|구성 요소가 설치되는 폴더입니다.| 컴퓨터의 모든 폴더|
|/MySQLCredsFilePath|필수|MySQL 서버 자격 증명이 저장되는 파일 경로입니다.|파일은 아래에 지정된 형식이어야 합니다.|
|/VaultCredsFilePath|필수|자격 증명 모음 자격 증명 파일의 경로입니다.|유효한 파일 경로|
|/EnvType|필수|보호하려는 환경 유형입니다. |VMware<br>NonVMware|
|/PSIP|필수|복제 데이터 전송에 사용할 NIC의 IP 주소입니다.| 모든 유효한 IP 주소|
|/CSIP|필수|구성 서버가 수신 대기하는 NIC의 IP 주소입니다.| 모든 유효한 IP 주소|
|/PassphraseFilePath|필수|암호 파일의 위치에 대한 전체 경로입니다.|유효한 파일 경로|
|/BypassProxy|선택 사항|구성 서버가 프록시 없이 Azure에 연결되도록 지정합니다.||
|/ProxySettingsFilePath|선택 사항|프록시 설정(인증이 필요한 기본 프록시 또는 사용자 지정 프록시)입니다.|파일은 아래에 지정된 형식이어야 합니다.|
|DataTransferSecurePort|선택 사항|복제 데이터에 사용할 PSIP의 포트 번호입니다.| 유효한 포트 번호(기본값: 9433)|
|/SkipSpaceCheck|선택 사항|캐시 디스크의 공간 확인을 건너뜁니다.| |
|/AcceptThirdpartyEULA|필수|플래그는 타사 EULA에 대한 동의를 의미합니다.| |
|/ShowThirdpartyEULA|선택 사항|타사 EULA를 표시합니다. 입력으로 제공되는 경우 다른 모든 매개 변수가 무시됩니다.| |

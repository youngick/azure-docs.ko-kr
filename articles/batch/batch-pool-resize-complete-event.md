---
title: Azure Batch 풀 크기 조정 완료 이벤트
description: Batch 풀 크기 조정 완료 이벤트에 대한 참조입니다. 크기가 늘어나고 성공적으로 완료된 풀의 예를 살펴봅니다.
ms.topic: reference
ms.date: 12/28/2020
ms.openlocfilehash: 9d3342587b5f6e0e134f4295a8c79deeb23df94b
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97803649"
---
# <a name="pool-resize-complete-event"></a>풀 크기 조정 완료 이벤트

 이 이벤트는 풀 크기 조정이 완료되거나 실패하면 내보내집니다.

 다음 예에서는 크기가 늘어나고 성공적으로 완료된 풀에 대한 풀 크기 조정 완료 이벤트의 본문을 보여 줍니다.

```
{
   "id": "myPool",
   "nodeDeallocationOption": "invalid",
      "currentDedicatedNodes": 10,
      "targetDedicatedNodes": 10,
   "currentLowPriorityNodes": 5,
     "targetLowPriorityNodes": 5,
   "enableAutoScale": false,
   "isAutoPool": false,
   "startTime": "2016-09-09T22:13:06.573Z",
   "endTime": "2016-09-09T22:14:01.727Z",
   "resultCode": "Success",
   "resultMessage": "The operation succeeded"
}
```

|요소|Type|메모|
|-------------|----------|-----------|
|`id`|String|풀의 ID입니다.|
|`nodeDeallocationOption`|String|풀 크기가 감소하는 경우 풀에서 노드를 제거할 수 있는 시기를 지정합니다.<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> **requeue** – 실행 중인 태스크를 종료하고 해당 태스크를 다시 대기열에 추가합니다. 작업이 활성화되면 태스크가 다시 실행됩니다. 태스크가 종료되는 즉시 노드를 제거합니다.<br /><br /> **terminate** – 실행 중인 태스크를 종료합니다. 태스크가 다시 실행되지 않습니다. 태스크가 종료되는 즉시 노드를 제거합니다.<br /><br /> **taskcompletion** – 현재 실행 중인 태스크가 완료될 때까지 기다립니다. 대기하는 동안 새 태스크를 예약하지 않습니다. 모든 태스크가 완료되면 노드를 제거합니다.<br /><br /> **Retaineddata** -현재 실행 중인 태스크가 완료될 때까지 기다린 후 모든 태스크 데이터 보존 기간이 만료될 때까지 기다립니다. 대기하는 동안 새 태스크를 예약하지 않습니다. 모든 태스크 보존 기간이 만료되면 노드를 제거합니다.<br /><br /> 기본값은 requeue입니다.<br /><br /> 풀 크기가 증가하는 경우 값이 **invalid** 로 설정됩니다.|
|`currentDedicatedNodes`|Int32|현재 풀에 할당된 전용 컴퓨팅 노드 수입니다.|
|`targetDedicatedNodes`|Int32|풀에 대해 요청된 전용 컴퓨팅 노드 수입니다.|
|`currentLowPriorityNodes`|Int32|현재 풀에 할당된 낮은 우선 순위 컴퓨팅 노드 수입니다.|
|`targetLowPriorityNodes`|Int32|풀에 대해 요청된 낮은 우선 순위 컴퓨팅 노드 수입니다.|
|`enableAutoScale`|Bool|풀 크기가 시간이 지남에 따라 자동으로 조정되는지 여부를 지정합니다.|
|`isAutoPool`|Bool|풀이 작업의 자동 풀 메커니즘을 통해 만들어졌는지 여부를 지정합니다.|
|`startTime`|DateTime|풀 크기 조정이 시작된 시간입니다.|
|`endTime`|DateTime|풀 크기 조정이 완료된 시간입니다.|
|`resultCode`|String|크기 조정의 결과입니다.|
|`resultMessage`|String| 결과에 대한 자세한 메시지입니다.<br /><br /> 크기 조정이 성공적으로 완료되면 작업에 성공했다고 표시됩니다.|

---
title: 릴리스 정보-음성 서비스
titleSuffix: Azure Cognitive Services
description: 음성 서비스 기능 릴리스, 향상 된 기능, 버그 수정 및 알려진 문제에 대 한 실행 로그입니다.
services: cognitive-services
author: oliversc
manager: jhakulin
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 03/18/2021
ms.author: oliversc
ms.custom: seodec18
ms.openlocfilehash: 86a656630f6c41e2cf6682d0160cce345d1f564d
ms.sourcegitcommit: 73d80a95e28618f5dfd719647ff37a8ab157a668
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2021
ms.locfileid: "105606626"
---
# <a name="speech-service-release-notes"></a>Speech Service 릴리스 정보

## <a name="speech-sdk-1160-2021-march-release"></a>Speech SDK 1.16.0:2021-3 월 릴리스

**참고**: Windows의 Speech SDK는 Visual Studio 2015, 2017 및 2019에 대 한 공유 Microsoft Visual C++ 재배포 가능 패키지에 따라 달라 집니다. [여기](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)에서 다운로드하세요.

**알려진 문제**

**C + +/c #/Java**: `DialogServiceConnector` 를 사용 `CustomCommandsConfig` 하 여 사용자 지정 명령 응용 프로그램에 액세스할 수 없으며 대신 연결 오류가 발생 합니다. 이 작업은를 사용 하 여 요청에 응용 프로그램 ID를 수동으로 추가 하 여 해결할 수 있습니다 `config.SetServiceProperty("X-CommandsAppId", "your-application-id", ServicePropertyChannel.UriQueryParameter)` . 의 예상 동작은 `CustomCommandsConfig` 다음 릴리스에서 복원 됩니다.

**하이라이트 요약**
- 메모리 및 디스크 공간을 줄여 SDK를 보다 효율적으로 만듭니다. 이번에는 Android에 집중 하 고 있습니다.
- 음성-텍스트와 텍스트 음성 변환 모두에 대 한 압축 오디오 지원 기능이 향상 되어 보다 효율적인 클라이언트/서버 통신을 만들 수 있습니다.
- 텍스트 음성 변환 음성을 말하는 애니메이션 문자는 이제 말하는 내용에 따라 lip와 얼굴을 자연스럽 게 이동할 수 있습니다.
- 새 기능 및 향상 된 기능을 통해 더 많은 사용 사례와 더 많은 구성에서 음성 SDK를 활용할 수 있습니다.
- 중요 한 고객의 문제를 해결 하기 위한 여러 버그 수정이 GitHub에 플래그를 지정 했습니다. 감사합니다! 의견을 보내 주시기 바랍니다.

#### <a name="new-features"></a>새로운 기능

- **C + +/c #/Java/Python**: GStreamer (1.18.3)의 최신 버전으로 이동 하 여 Windows, Linux 및 Android의 _모든_ 미디어 형식에 대 한 지원을 추가 합니다. [여기](https://docs.microsoft.com/azure/cognitive-services/speech-service/how-to-use-codec-compressed-audio-input-streams)에서 설명서를 참조 하세요. 이전에는 SDK에서 지원 되는 GStreamer 형식의 하위 집합만 지원 했습니다. 이를 통해 사용 사례에 적합 한 오디오 형식을 유연 하 게 사용할 수 있습니다.
- **C + +/c #/Java/Objective-C/Python**: 압축 된 TTS/합성 오디오를 SDK와 디코딩하는 지원을 추가 했습니다. 출력 오디오 형식을 PCM으로 설정 하 고 시스템에서 GStreamer를 사용할 수 있는 경우 SDK는 서비스에서 압축 된 오디오를 자동으로 요청 하 여 대역폭을 절약 하 고 클라이언트에서 오디오를 디코딩합니다. 이렇게 하면 사용 사례에 필요한 대역폭을 낮출 수 있습니다. `SpeechServiceConnection_SynthEnableCompressedAudioTransmission`을로 설정 `false` 하 여이 기능을 사용 하지 않도록 설정할 수 있습니다. [C + +](https://docs.microsoft.com/cpp/cognitive-services/speech/microsoft-cognitiveservices-speech-namespace#propertyid), [c #](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.propertyid?view=azure-dotnet), [Java](https://docs.microsoft.com/java/api/com.microsoft.cognitiveservices.speech.propertyid?view=azure-java-stable), [목표-C](https://docs.microsoft.com/objectivec/cognitive-services/speech/spxpropertyid), [Python](https://docs.microsoft.com/python/api/azure-cognitiveservices-speech/azure.cognitiveservices.speech.propertyid?view=azure-python)에 대 한 세부 정보입니다.
- **JavaScript** Node.js: 사용자는 이제 API를 사용할 수 있으며,이 [ `AudioConfig.fromWavFileInput` API](https://docs.microsoft.com/javascript/api/microsoft-cognitiveservices-speech-sdk/audioconfig?view=azure-node-latest#fromWavFileInput_File_)를 통해 고객은 디스크의 경로를 .wav 파일로 wav 파일에 보낼 수 있습니다. 그러면 sdk가이를 인식할 수 있습니다. 이 [#252 GitHub 문제](https://github.com/microsoft/cognitive-services-speech-sdk-js/issues/252)를 해결 합니다.
- **C + +/c #/Java/Objective-C/Python**: `GetVoicesAsync()` 사용 가능한 모든 합성 음성을 프로그래밍 방식으로 반환 하는 TTS에 대 한 메서드를 추가 했습니다. 이렇게 하면 응용 프로그램에서 사용 가능한 음성을 나열 하거나 프로그래밍 방식으로 다른 음성에서 선택할 수 있습니다. [C + +](https://docs.microsoft.com/cpp/cognitive-services/speech/speechsynthesizer#getvoicesasync), [c #](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.speechsynthesizer?view=azure-dotnet#methods), [Java](https://docs.microsoft.com/java/api/com.microsoft.cognitiveservices.speech.speechsynthesizer?view=azure-java-stable#methods), [목표-C](https://docs.microsoft.com/objectivec/cognitive-services/speech/spxspeechsynthesizer#getvoices)및 [Python](https://docs.microsoft.com/python/api/azure-cognitiveservices-speech/azure.cognitiveservices.speech.speechsynthesizer?view=azure-python#methods)에 대 한 세부 정보입니다.
- **C + +/c #/Java/JavaScript/Objective-C/Python**: 지원 되 `VisemeReceived` 는 TTS/음성 합성 이벤트를 추가 하 여 동기 viseme 애니메이션을 반환 합니다. Visemes를 사용 하면 보다 자연 스런 뉴스 브로드캐스트 길잡이, 더 많은 대화형 게임 및 만화 문자 및 보다 직관적인 언어 교육 비디오를 만들 수 있습니다. 청각 장애가 있는 사용자는 소리를 시각적으로 선택 하 고 음성 콘텐츠를 "립-읽기" 할 수도 있습니다. [여기](https://docs.microsoft.com/azure/cognitive-services/speech-service/how-to-speech-synthesis-viseme)에서 설명서를 참조 하세요.
- **C + +/c #/Java/JavaScript/Objective-C/Python**: `BookmarkReached` TTS에 대 한 이벤트를 추가 했습니다. 입력 SSML에서 책갈피를 설정 하 고 각 책갈피에 대 한 오디오 오프셋을 가져올 수 있습니다. 응용 프로그램에서이를 사용 하 여 특정 단어가 텍스트를 음성으로 말할 때 작업을 수행할 수 있습니다. [여기](https://docs.microsoft.com/azure/cognitive-services/speech-service/speech-synthesis-markup#bookmark-element)에서 설명서를 참조 하세요.
- **Java**: java에서 스피커 인식을 사용할 수 있도록 하는 스피커 인식 api에 대 한 지원이 추가 되었습니다. 자세한 내용은 [여기](https://docs.microsoft.com/java/api/com.microsoft.cognitiveservices.speech.speakerrecognizer?view=azure-java-stable)를 참조 하세요.
- **C + +/c #/Java/JavaScript/Objective-C/Python**: TTS 용 webm 컨테이너 (Webm16Khz16BitMonoOpus 및 Webm24Khz16BitMonoOpus)를 사용 하 여 두 개의 새로운 출력 오디오 형식을 추가 했습니다. 이러한 형식은 Opus 코덱으로 오디오를 스트리밍하는 데 더 적합 합니다. [C + +](https://docs.microsoft.com/cpp/cognitive-services/speech/microsoft-cognitiveservices-speech-namespace#speechsynthesisoutputformat), [c #](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.speechsynthesisoutputformat?view=azure-dotnet), [Java](https://docs.microsoft.com/java/api/com.microsoft.cognitiveservices.speech.speechsynthesisoutputformat?view=azure-java-stable), [JavaScript](https://docs.microsoft.com/javascript/api/microsoft-cognitiveservices-speech-sdk/speechsynthesisoutputformat?view=azure-node-latest), [목표-c](https://docs.microsoft.com/objectivec/cognitive-services/speech/spxspeechsynthesisoutputformat), [Python](https://docs.microsoft.com/python/api/azure-cognitiveservices-speech/azure.cognitiveservices.speech.speechsynthesisoutputformat?view=azure-python)에 대 한 세부 정보입니다.
- **C + +/c #/Java/Python**: 인증서 해지 목록에 대 한 네트워크 액세스를 차단 하는 환경에서 연결이 성공 하도록 Linux에 대 한 지원이 추가 되었습니다. 이렇게 하면 클라이언트 컴퓨터에서 Azure Speech service에만 연결 하도록 선택할 수 있습니다. [여기](https://docs.microsoft.com/azure/cognitive-services/speech-service/how-to-configure-openssl-linux)에서 설명서를 참조 하세요.
- **C + +/c #/Java**: 앱이 스피커 데이터를 기존 음성 프로필과 비교할 수 있도록 스피커 인식 시나리오용 음성 프로필 검색에 대 한 지원이 추가 되었습니다. [C + +](https://docs.microsoft.com/cpp/cognitive-services/speech/speakerrecognizer), [c #](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.speakerrecognizer?view=azure-dotnet)및 [Java](https://docs.microsoft.com/java/api/com.microsoft.cognitiveservices.speech.speakerrecognizer?view=azure-java-stable)에 대 한 세부 정보입니다. 이 [#808 GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/808)를 해결 합니다.
- **목적-C/Swift**: 파라솔 헤더를 사용 하 여 모듈 프레임 워크에 대 한 지원이 추가 되었습니다. 이를 통해 iOS/Mac 목표-C/Swift apps에서 음성 SDK를 모듈로 가져올 수 있습니다. 이 [#452 GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/452)를 해결 합니다.
- **Python**: python [3.9](https://docs.microsoft.com/azure/cognitive-services/speech-service/quickstarts/setup-platform?pivots=programming-language-python) 에 대 한 지원이 추가 되 고 python의 최신 [3.5 용 종료](https://devguide.python.org/devcycle/#end-of-life-branches)에 대 한 3.5 지원이 삭제 되었습니다.

#### <a name="improvements"></a>향상 된 기능

- **Java**: 음성 SDK의 메모리 사용량 및 디스크 공간을 줄이기 위한 다중 릴리스 노력의 일환으로 Android 바이너리가 이제 3%에서 5% 더 작습니다.
- **C #**: c #에서 SDK의 [유용성을 개선 하기 위해](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech?view=azure-dotnet) c # 참조 설명서의 향상 된 정확도, 가독성 및 참조 섹션도 향상 되었습니다.
- **C + +/c #/Java/Objective-C/Python**: 마이크 및 스피커 컨트롤을 별도의 공유 라이브러리로 이동 했습니다. 이렇게 하면 오디오 하드웨어가 필요 하지 않은 사용 사례에서 SDK를 사용할 수 있습니다. 예를 들어 Linux에서 사용 사례에 대 한 마이크나 스피커가 필요 하지 않은 경우 libasound를 설치할 필요가 없습니다.

#### <a name="bug-fixes"></a>버그 수정

- **JavaScript**: 이제 긴 WAV 파일 헤더가 올바르게 구문 분석 됩니다 (헤더 조각을 512 바이트로 늘립니다). 이 [#962 GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/962)를 해결 합니다.
- **JavaScript**: 인식 중지 전에 mic 스트림이 종료 되어 Firefox에서 작동 하지 않는 음성 인식 문제를 해결 하는 경우 마이크 타이밍 문제가 수정 되었습니다.
- **JavaScript**: 이제 turnOn 완료 되기 전에 브라우저에서 mic를 강제로 실행 하면 초기화 약속을 올바르게 처리 합니다.
- **JavaScript**: url 종속성을 url 구문 분석으로 대체 했습니다. 이 [#264 GitHub 문제](https://github.com/microsoft/cognitive-services-speech-sdk-js/issues/264)를 해결 합니다.
- **Android**: `minifyEnabled` 가 true로 설정 된 경우 콜백이 작동 하지 않는 문제를 수정 했습니다.
- **C + +/c #/Java/Objective-C/Python**: `TCP_NODELAY` 대기 시간을 줄이기 위해 TTS의 기본 소켓 IO로 올바르게 설정 됩니다.
- **C + +/c #/Java/Python/Objective-C/Go**: 인식을 시작한 후 인식기가 삭제 되었을 때 발생 하는 간헐적 충돌을 수정 했습니다.
- **C + +/c #/Java**: 스피커 인식기가 소멸 될 때 가끔 충돌이 해결 되었습니다.

#### <a name="samples"></a>샘플

- **Javascript**: [브라우저 샘플](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/js/browser) 은 더 이상 별도 JavaScript 라이브러리 파일 다운로드를 요구 하지 않습니다.

## <a name="speech-cli-also-known-as-spx-2021-march-release"></a>Speech CLI (SPX 라고도 함): 2021-3 월 릴리스

**참고**: [여기](https://docs.microsoft.com/azure/cognitive-services/speech-service/spx-basics)에서 Azure Speech service CLI (명령줄 인터페이스)를 시작 하세요. CLI를 사용 하면 코드를 작성 하지 않고도 Azure Speech service를 사용할 수 있습니다.

#### <a name="new-features"></a>새로운 기능

- `spx intent`의도 인식, 바꾸기 명령이 추가 되었습니다 `spx recognize intent` .
- 이제를 사용 하 여 인식 및 의도가 Azure 함수를 사용 하 여 단어 오류 요금을 계산할 수 있습니다 `spx recognize --wer url <URL>` .
- 이제 Recognize는를 사용 하 여 결과를 VTT 파일로 출력할 수 있습니다 `spx recognize --output vtt file <FILENAME>` .
- 중요 한 키 정보는 이제 디버그/자세한 정보 출력에 가려져 있습니다.
- 일괄 처리 기록 만들기의 콘텐츠 필드에 대 한 URL 검사 및 오류 메시지를 추가 했습니다.

**Covid-19 요약 테스트**:

진행 중인 전염병는 엔지니어가 집에서 작업 하는 데 계속 필요 하므로 사전 전염병 수동 확인 스크립트가 크게 줄었습니다. 구성 수가 더 적고 환경 특정 버그가 지연 될 가능성이 더 낮은 장치에서 테스트 합니다. 여전히 많은 자동화를 사용 하 여 엄격한 유효성 검사를 수행 합니다. 오류가 발생 하지 않은 경우 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen)에서 알려주세요.<br>
정상 상태를 유지 하세요.



## <a name="speech-sdk-1150-2021-january-release"></a>Speech SDK 1.15.0:2021-1 월 릴리스

**참고**: Windows의 Speech SDK는 Visual Studio 2015, 2017 및 2019에 대 한 공유 Microsoft Visual C++ 재배포 가능 패키지에 따라 달라 집니다. [여기](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)에서 다운로드하세요.

**하이라이트 요약**
- 메모리 및 디스크 공간을 줄여서 SDK를 보다 효율적으로 만듭니다.
- 사용자 지정 신경망 비공개 미리 보기에 사용할 수 있는 고품질 출력 형식입니다.
- 이제 의도 인식기가 최고 의도 보다 더 많이 돌아올 수 있으므로 고객의 의도에 대 한 별도의 평가를 수행할 수 있습니다.
- 이제 음성 도우미 나 봇을 보다 쉽게 설정할 수 있으며, 즉시 수신 대기를 중지 하 고 오류에 대응 하는 방법을 보다 효과적으로 제어할 수 있습니다.
- 압축을 선택 하 여 장치 성능이 향상 되었습니다.
- Windows ARM/ARM64에서 Speech SDK를 사용 합니다.
- 낮은 수준의 디버깅이 향상 되었습니다.
- 이제 음성 음성 기능을 보다 폭넓게 사용할 수 있습니다.
- 중요 한 고객의 문제를 해결 하기 위한 여러 버그 수정이 GitHub에 플래그를 지정 했습니다. 감사합니다! 의견을 보내 주시기 바랍니다.

**개선과**
- 이제 Speech SDK는 더 효율적이 고 간단 합니다. 음성 SDK의 메모리 사용량 및 디스크 공간을 줄이기 위해 여러 릴리스 작업을 시작 했습니다. 첫 번째 단계로 대부분의 플랫폼에서 공유 라이브러리의 중요 한 파일 크기를 단축 했습니다. 1.14 릴리스와 비교:
  - 64 비트 UWP 호환 Windows 라이브러리는 약 30% 더 작습니다.
  - 32 비트 Windows 라이브러리는 아직 크기를 개선 하지 않습니다.
  - Linux 라이브러리는 20-25% 더 작습니다.
  - Android 라이브러리는 3-5% 더 작습니다.

**새로운 기능**
- **모두**: TTS 음성 합성 API를 통해 사용자 지정 신경망의 비공개 미리 보기에 사용할 수 있는 새 48khz 출력 형식: Audio48Khz192KBitRateMonoMp3, audio-48khz-192kbitrate 전송률-mono-Mp3, Audio48Khz96KBitRateMonoMp3, audio-48khz-96kbitrate 전송률-mono-Mp3, Raw48Khz16BitMonoPcm, raw-48khz-16 비트-Mono, Riff48Khz16BitMonoPcm, riff-48khz-16 비트-mono-pcm.
- **모든**: 사용자 지정 음성도 더 쉽게 사용할 수 있습니다. 사용자 지정 음성 via `EndpointId` ([c + +](/cpp/cognitive-services/speech/speechconfig#setendpointid), [c #](/dotnet/api/microsoft.cognitiveservices.speech.speechconfig.endpointid#Microsoft_CognitiveServices_Speech_SpeechConfig_EndpointId), [Java](/java/api/com.microsoft.cognitiveservices.speech.speechconfig.setendpointid#com_microsoft_cognitiveservices_speech_SpeechConfig_setEndpointId_String_), [JavaScript](/javascript/api/microsoft-cognitiveservices-speech-sdk/speechconfig#endpointId), [목표-C](/objectivec/cognitive-services/speech/spxspeechconfiguration#endpointid), [Python](/python/api/azure-cognitiveservices-speech/azure.cognitiveservices.speech.speechconfig#endpoint-id))를 설정 하기 위한 지원이 추가 되었습니다. 이 변경 전에 사용자 지정 음성 사용자는 메서드를 통해 끝점 URL을 설정 해야 합니다 `FromEndpoint` . 이제 고객이 `FromSubscription` 공용 음성 처럼 메서드를 사용 하 고를 설정 하 여 배포 id를 제공할 수 있습니다 `EndpointId` . 이렇게 하면 사용자 지정 음성 설정이 간단해 집니다. 
- **C + +/c #/Java/Objective-C/Python**:에서 가장 많이 발생 하는 의도 이상의 의도를 가져옵니다 `IntentRecognizer` . 이제 `LanguageUnderstandingModel FromEndpoint` uri 매개 변수를 사용 하 여 메서드를 통한 상위 점수 매기기 의도가 아니라 모든 의도를 포함 하는 JSON 결과 구성을 지원 `verbose=true` 합니다. 이 [#880 GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/880)를 해결 합니다. [여기](./quickstarts/intent-recognition.md#add-a-languageunderstandingmodel-and-intents)에서 업데이트 된 설명서를 참조 하세요.
- **C + +/c #/Java**: 음성 길잡이나 봇이 immediatedly 수신을 중지 하도록 합니다. `DialogServiceConnector` ([C + +](/cpp/cognitive-services/speech/dialog-dialogserviceconnector), [c #](/dotnet/api/microsoft.cognitiveservices.speech.dialog.dialogserviceconnector), [Java](/java/api/com.microsoft.cognitiveservices.speech.dialog.dialogserviceconnector))에는 이제 `StopListeningAsync()` 함께 제공할 메서드가 있습니다 `ListenOnceAsync()` . 그러면 오디오 캡처가 즉시 중지 되 고 결과가 정상적으로 대기 하 여 "지금 중지" 단추 누르기 시나리오와 함께 사용 하기에 적합 합니다.
- **C + +/c #/Java/JavaScript**: 기본 시스템 오류에 대해 음성 도우미 또는 봇이 더 잘 반응 하도록 합니다. `DialogServiceConnector` ([C + +](/cpp/cognitive-services/speech/dialog-dialogserviceconnector), [c #](/dotnet/api/microsoft.cognitiveservices.speech.dialog.dialogserviceconnector), [Java](/java/api/com.microsoft.cognitiveservices.speech.dialog.dialogserviceconnector), [JavaScript](/javascript/api/microsoft-cognitiveservices-speech-sdk/dialogserviceconnector))에는 이제 새 `TurnStatusReceived` 이벤트 처리기가 있습니다. 이러한 선택적 이벤트는 [`ITurnContext`](/dotnet/api/microsoft.bot.builder.iturncontext) Bot의 모든 해상도에 해당 하며, 발생 하는 경우 실행 실패를 보고 합니다. 예를 들어 처리 되지 않은 예외, 시간 제한 또는 직접 줄 음성 및 봇 간의 네트워크 drop의 결과로 발생 합니다. `TurnStatusReceived` 를 사용 하면 오류 조건에 더 쉽게 대응할 수 있습니다. 예를 들어, 봇이 백 엔드 데이터베이스 쿼리 (예: 제품 조회)에 너무 오래 걸리는 경우 `TurnStatusReceived` 클라이언트는 "죄송 합니다. 다시 시도할 수 있습니다." 라는 메시지가 표시 될 수 있습니다.
- **C + +/c #**: 더 많은 플랫폼에서 음성 SDK를 사용 합니다. 이제 [SPEECH sdk nuget 패키지](https://www.nuget.org/packages/Microsoft.CognitiveServices.Speech) 는 Windows ARM/ARM64 desktop 네이티브 이진 파일 (UWP가 이미 지원 됨)을 지원 하기 때문에 더 많은 컴퓨터 형식에서 음성 sdk를 더 유용 하 게 사용할 수 있습니다.
- **Java**: [`DialogServiceConnector`](/java/api/com.microsoft.cognitiveservices.speech.dialog.dialogserviceconnector) 이제 이전에 `setSpeechActivityTemplate()` 언어에서 실수로 제외 된 메서드가 있습니다. 이는 속성을 설정 하는 것과 동일 `Conversation_Speech_Activity_Template` 하며, 직접 라인 음성 서비스에서 발생 한 모든 향후 봇 프레임 워크 활동은 제공 된 콘텐츠를 해당 JSON 페이로드에 병합 하도록 요청 합니다.
- **Java**: 낮은 수준의 디버깅이 향상 되었습니다. [`Connection`](/java/api/com.microsoft.cognitiveservices.speech.connection)이제 클래스에는 `MessageReceived` 다른 프로그래밍 언어와 유사한 이벤트가 있습니다 (c + +, c #). 이 이벤트는 서비스에서 들어오는 데이터에 대 한 하위 수준 액세스를 제공 하며 진단 및 디버깅에 유용할 수 있습니다.
- **JavaScript**: [`BotFrameworkConfig`](/javascript/api/microsoft-cognitiveservices-speech-sdk/botframeworkconfig) 이제 `fromHost()` `fromEndpoint()` 사용자 지정 서비스 위치를 편리 하 게 설정 하 고 속성을 설정 하는 방법 및 팩터리 메서드를 사용 하는 및 팩터리 메서드를 사용 하 여 음성 도우미와 봇을 쉽게 설정할 또한 `botId` 구성 팩터리에 대해 기본이 아닌 봇을 사용 하기 위해의 선택적 사양을 표준화 합니다.
- **JavaScript**: websocket 압축을 위해 추가 된 문자열 제어 속성을 통해 장치 성능이 개선 되었습니다. 성능상의 이유로, 기본적으로 websocket 압축을 사용 하지 않도록 설정 했습니다. 낮은 대역폭 시나리오에 대 한 했다가 다시 설정할 수 있습니다. 자세한 내용은 [여기](/javascript/api/microsoft-cognitiveservices-speech-sdk/propertyid)에 있습니다. 이 [#242 GitHub 문제](https://github.com/microsoft/cognitive-services-speech-sdk-js/issues/242)를 해결 합니다.
- **JavaScript**: 음성 발음을 평가할 수 있도록 발음 평가에 대 한 지원이 추가 되었습니다. [여기](./how-to-pronunciation-assessment.md?pivots=programming-language-javascript)에서 빠른 시작을 참조 하세요.

**버그 수정**
- **모두** (JavaScript 제외): 인식기에서 너무 많은 메모리를 할당 한 버전 1.14에서 회귀를 수정 했습니다.
- **C + +**:에서의 가비지 수집 문제 `DialogServiceConnector` 를 해결 하 고 [GitHub 문제 #794](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/794)해결 합니다.
- **C #**: 삭제 시 개체가 두 번째에 대해 차단 되도록 하는 스레드 종료와 관련 된 문제를 해결 했습니다.
- **C + +/c #/Java**: 응용 프로그램이에서 음성 권한 부여 토큰 또는 활동 템플릿을 두 번 이상 설정 하는 것을 방지 하는 예외를 수정 했습니다 `DialogServiceConnector` .
- **C + +/c #/Java**: 해체의 경합 상태로 인 한 인식기 충돌을 수정 했습니다.
- **JavaScript**: [`DialogServiceConnector`](/javascript/api/microsoft-cognitiveservices-speech-sdk/dialogserviceconnector) `botId` 의 팩터리에 지정 된 선택적 매개 변수를 이전에 인식 하지 못했습니다 `BotFrameworkConfig` . 이 경우 `botId` 기본이 아닌 봇을 사용 하도록 쿼리 문자열 매개 변수를 수동으로 설정 해야 했습니다. 버그가 수정 되었고 `botId` 공장에 제공 된 값 `BotFrameworkConfig` 이 신규 및 추가를 포함 하 여 사용 및 사용 됩니다 `fromHost()` `fromEndpoint()` . 이는 `applicationId` 에 대 한 매개 변수에도 적용 됩니다 `CustomCommandsConfig` .
- **JavaScript**: [GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/881)를 수정 했습니다. 인식기 개체를 다시 사용 하도록 허용 하는 #881.
- **JavaScript**: `speech.config` 하나의 TTS 세션에서 SKD를 여러 번 전송 하 여 대역폭을 낭비 하는 문제를 해결 했습니다.
- **JavaScript**: 마이크 권한 부여에 대 한 오류 처리를 간소화 하 여 사용자가 브라우저에서 마이크 입력을 허용 하지 않는 경우 더 많은 설명 메시지를 표시할 수 있도록 합니다.
- **JavaScript**:에서 형식 오류가 발생 하 고 [](https://github.com/microsoft/cognitive-services-speech-sdk-js/issues/249) `ConversationTranslator` `ConversationTranscriber` TypeScript 사용자에 대 한 컴파일 오류가 발생 하는 #249 GitHub 문제가 수정 되었습니다.
- GStreamer: Xcode 11.4에서 iOS에 대 한 빌드에 실패 하는 문제를 해결 [#911 GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/911)를 해결 **합니다.**
- **Python**: [GitHub 문제 #870](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/870)수정, "DeprecationWarning: 맞도록 of importlib에서 imp 모듈이 더 이상 사용 되지 않습니다."

**샘플**
- [JavaScript 브라우저의 파일 기반 샘플](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/quickstart/javascript/browser/from-file/index.html) 은 이제 음성 인식을 위해 파일을 사용 합니다. 이 [#884 GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/884)를 해결 합니다.

## <a name="speech-cli-also-known-as-spx-2021-january-release"></a>Speech CLI (SPX 라고도 함): 2021-1 월 릴리스

**새로운 기능**
- 이제 Speech CLI를 [NuGet 패키지로](https://www.nuget.org/packages/Microsoft.CognitiveServices.Speech.CLI/) 사용할 수 있으며, shell/명령줄에서 호출할 수 있는 .net 전역 도구로 .net cli를 통해 설치할 수 있습니다.
- [Custom Speech DevOps 템플릿 리포지토리](https://github.com/Azure-Samples/Speech-Service-DevOps-Template) 는 Custom Speech 워크플로에 대해 음성 CLI를 사용 하도록 업데이트 되었습니다.

**Covid-19 요약 테스트**: 지속적인 전염병 엔지니어가 집에서 작업 하는 데 계속 필요 하므로 사전 전염병 수동 확인 스크립트가 크게 줄었습니다. 구성 수가 더 적고 환경 특정 버그가 지연 될 가능성이 더 낮은 장치에서 테스트 합니다. 여전히 많은 자동화를 사용 하 여 엄격한 유효성 검사를 수행 합니다. 오류가 발생 하지 않은 경우 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen)에서 알려주세요.<br>
정상 상태를 유지 하세요.

## <a name="text-to-speech-2020-december-release"></a>텍스트 음성 변환 2020-12 월 릴리스

**GA 및 미리 보기의 새로운 신경망**

54 언어/로캘에서 전체 129 신경망에 대해 51 새로운 음성이 발표 되었습니다.

- **46 GA 로캘의 새 음성**: Shakir `ar-EG` (이집트), Hamed `ar-SA` 아랍어 (사우디아라비아), Borislav의 `bg-BG` 불가리아어 (불가리아), Joana의 ( `ca-ES` 스페인), `cs-CZ` 체코어 (체코 공화국) 덴마크어 (덴마크)의 Jeppe, `da-DK` `de-AT` 독일어 (오스트리아), 1 월 `de-CH` 독일어 (스위스), nestoras 그리스어 (그리스), `el-GR` Liam (영어, `en-CA` 캐나다), Jonas 또는 영어 (아일랜드), Madhur (인도)의, 인도 (인도)의 `en-IE` `en-IN` Monabhat (인도) `en-IN` `en-IN` 타밀어 (인도)의 valluvar, `en-IN` Enric `es-ES` (스페인), 에스토니아어 (에스토니아)의 Kert, 핀란드의 Harri, 핀란드 `et-EE` `fi-FI` `fi-FI` (핀란드), 핀란드에서 Fabrice `fr-CH` (스위스),의 colm ( `ga-IE` 아일랜드), Avri In `he-IL` 히브리어 (이스라엘), `hr-HR` 크로아티아어 (크로아티아어), 크로아티아어 (크로아티아어), 헝가리 (Tamas), 헝가리의 Gadis, 인도네시아 (인도네시아), Joseph의 `hu-HU` `id-ID` `lt-LT` nils, `lv-LV` 라트비아 (라트비아), Osman의 ( `ms-MY` 말레이시아),의 `mt-MT` (몰타) , 노르웨이어, 복말 (노르웨이), Pernille 노르웨이어, 복말 (노르웨이), 네덜란드어 (네덜란드), 네덜란드어 (네덜란드), 네덜란드어 (네덜란드), 폴란드어 (네덜란드), 폴란드어 (폴란드어)의 Fenna, 폴란드어 (폴란드어)의 `nb-NO` `nb-NO` `nl-NL` `nl-NL` `pl-PL` Marek, `pl-PL` 포르투갈어 (브라질)의 dute, 포르투갈어 ( `pt-BR` 브라질)의 Raquel `pt-PT` `ro-RO` `ru-RU` 러시아 (러시아)의 Svetlana, 슬로바키아어 (슬로바키아)의 Rok (슬로바키아), 슬로베니아어 (슬로베니아)의 Mattias, 스웨덴어 (스웨덴), 스웨덴어 (스웨덴), `ru-RU` `sk-SK` `sl-SI` `sv-SE` Sofie의 Niwat (태국), `sv-SE` Ahmet ( `th-TH` 터키) `tr-TR` ), NamMinh에서 `vi-VN` 베트남어 (베트남), HsiaoChen `zh-TW` 대만 북경어 (대만), yunjhe In 대만 북경어 (대만), 중국어 (홍콩) in 중국어 광둥어 (홍콩) `zh-TW` `zh-HK` , WanLung in `zh-HK` 중국어 광둥어 (홍콩)

- **미리 보기 로캘에서 새로** 제공 되는 새 음성: `et-EE` 에스토니아어 (에스토니아)의 Kert, 아일랜드의 Colm `ga-IE` (아일랜드), 아일랜드의 nils ( `lv-LV` 라트비아), 리투아니아어 (리투아니아)의 leonas ( `lt-LT` 리투아니아), `mt-MT` 몰타어 (몰타) Joseph).

이번 릴리스에서는 54 언어/로캘에서 전체 129 신경망을 지원 합니다. 또한 70 이상의 표준 음성이 49 언어/로캘에서 제공 됩니다. 전체 목록에 대 한 [언어 지원](language-support.md#text-to-speech) 을 방문 하세요.

**오디오 콘텐츠 만들기에 대 한 업데이트**
- 음성 범주 및 자세한 음성 설명이 포함 된 음성 선택 UI가 개선 되었습니다. 
- 여러 언어의 모든 신경망에 대해 intonation 튜닝을 사용 하도록 설정 했습니다.
- 브라우저의 언어에 따라 UI localizaiton를 자동화 합니다.
- `StyleDegree`모든 신경망에 대해 컨트롤을 사용할 수 `zh-CN` 있습니다.
[오디오 콘텐츠 만들기 도구](https://speech.microsoft.com/audiocontentcreation) 를 방문 하 여 새로운 기능을 확인 하세요. 

**Zh-cn에 대 한 업데이트-CN 음성**
- `zh-CN`영어 말하기를 지원 하도록 모든 신경망을 업데이트 했습니다.
- `zh-CN`Intonation 조정을 지원 하도록 모든 신경망을 사용 하도록 설정 했습니다. SSML 또는 오디오 콘텐츠 생성 도구를 사용 하 여 가장 적합 한 intonation를 조정할 수 있습니다.
- 모든 `zh-CN` 다중 스타일의 신경망이 컨트롤을 지원 하도록 업데이트 되었습니다 `StyleDegree` . Emotion 강도 (soft 또는 strong)를 조정할 수 있습니다.
- `zh-CN-YunyeNeural`다른 감정을를 수행할 수 있는 여러 스타일을 지원 하도록 업데이트 되었습니다.

## <a name="text-to-speech-2020-november-release"></a>텍스트 음성 변환 2020-11 월 릴리스

**새 로캘 및 미리 보기의 음성**
- 신경망 **5 개의 새 음성 및 언어가** 신경망에 도입 되었습니다. 이러한 작업은 몰타어 (몰타)의 유예, 리투아니아 (리투아니아),로 마이그레이션의 Anu, 에스토니아어 (에스토니아), 아일랜드의 Orla (아일랜드) 및 Everita (라트비아)의입니다.
- **`zh-CN` 여러 스타일 및 역할이 있는 새 음성 5** 개 (Xiaohan, Xiaomo, Xiaorui, Xiaoxuan 및 yunxi)를 지원 합니다.

> 이러한 음성은 SouthEastAsia 및 WestEurope의 세 가지 Azure 지역에서 공개 미리 보기로 제공 됩니다.

**신경망 컨테이너 GA**
- 신경망 컨테이너를 사용 하면 개발자는 특정 보안 및 데이터 관리 요구 사항에 맞게 자신의 환경에서 가장 자연 스러운 디지털 음성이 포함 된 음성 합성을 실행할 수 있습니다. [음성 컨테이너를 설치 하는 방법을](speech-container-howto.md)확인 합니다. 

**새로운 기능**
- **사용자 지정 음성**: 한 지역에서 다른 지역으로 음성 모델을 복사 하는 enabed 사용자 끝점 일시 중단 및 다시 시작이 지원 됩니다. 여기에서 [포털로](https://speech.microsoft.com/customvoice) 이동 합니다.
- [SSML 대기 태그](speech-synthesis-markup.md#add-silence) 지원. 
- 일반 TTS 음성 품질 향상: nb에서 향상 된 단어 수준 발음 정확도입니다. 53%의 발음 오류가 감소 했습니다.

> [이 기술 블로그에서](https://techcommunity.microsoft.com/t5/azure-ai/neural-text-to-speech-previews-five-new-languages-with/ba-p/1907604)자세한 내용을 알아보세요.

## <a name="text-to-speech-2020-october-release"></a>텍스트 음성 변환 2020-10 월 릴리스

**새로운 기능**
- 의는 새 스타일을 지원 `newscast` 합니다. [SSML에서 말하는 스타일을 사용 하는 방법을](speech-synthesis-markup.md#adjust-speaking-styles)참조 하세요.
- **오디오 충실도를 높이고 더 빠른 합성 속도를 사용 하 여 vocoder로 업그레이드 한 신경망** 입니다. 이를 통해 해당 시나리오는 비디오 dubbing, 오디오 서적 또는 온라인 교육 자료를 비롯 한 긴 fi 오디오 또는 긴 상호 작용을 사용 하는 고객에 게 유용 합니다. [기술 커뮤니티 블로그에서 스토리에 대해 자세히 읽고 음성 샘플 듣기](https://techcommunity.microsoft.com/t5/azure-ai/azure-neural-tts-upgraded-with-hifinet-achieving-higher-audio/ba-p/1847860)
- **17 개 로캘로 지역화 된 [사용자 지정 음성](https://speech.microsoft.com/customvoice)  &  [오디오 콘텐츠 생성 스튜디오](https://speech.microsoft.com/audiocontentcreation)** 입니다. 사용자는 보다 친숙 한 환경을 위해 UI를 로컬 언어로 쉽게 전환할 수 있습니다.   
- **오디오 콘텐츠 만들기**: XiaoxiaoNeural에 대 한 스타일 수준 제어를 추가 했습니다. 50ms의 증분 나누기를 포함 하도록 사용자 지정 된 중단 기능을 구체화 했습니다. 

**일반 TTS 음성 품질 향상**
- 에서 향상 된 단어 수준 발음 정확도 `pl-PL` (오류 발생률 감소: 51%) 및 `fi-FI` (오류 발생률 감소: 58%)
- `ja-JP`사전 시나리오에 대 한 단일 단어 읽기 기능이 향상 되었습니다. 발음 오류가 80% 감소 했습니다.
- `zh-CN-XiaoxiaoNeural`: 감정/CustomerService/Newscast/Cheerful/화난 스타일의 음성 품질이 향상 되었습니다.
- `zh-CN`: Intelligibility를 크게 향상 시키는 Erhua 발음 및 밝은 톤과 구체화 된 공간 prosody를 개선 했습니다. 

## <a name="speech-sdk-1140-2020-october-release"></a>Speech SDK 1.14.0:2020-10 월 릴리스

**참고**: Windows의 Speech SDK는 Visual Studio 2015, 2017 및 2019에 대 한 공유 Microsoft Visual C++ 재배포 가능 패키지에 따라 달라 집니다. [여기](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)에서 다운로드하세요.

**새로운 기능**
- **Linux**: Debian 10 및 Ubuntu 20.04 lts에 대 한 지원이 추가 되었습니다.
- **Python/목표-C**: API에 대 한 지원이 추가 되었습니다 `KeywordRecognizer` . 설명서는 [여기](./custom-keyword-basics.md)에 있습니다.
- **C + +/Java/C #**:를 `HttpHeader` 통해 키/값을 설정 하는 지원이 추가 되었습니다 `ServicePropertyChannel::HttpHeader` .
- **JavaScript**: API에 대 한 지원이 추가 되었습니다 `ConversationTranscriber` . [여기](./how-to-use-conversation-transcription.md?pivots=programming-language-javascript)에서 설명서를 참조 하세요. 
- **C + +/c #**: 새 `AudioDataStream FromWavFileInput` 메서드 (읽기)를 추가 했습니다. WAV 파일) [여기 (c + +)](/cpp/cognitive-services/speech/audiodatastream) 및 [여기 (c #)](/dotnet/api/microsoft.cognitiveservices.speech.audiodatastream)를 참조 하세요.
-  **C + +/c #/Java/Python/Objective-C/Swift**: `stopSpeakingAsync()` 텍스트-음성 합성을 중지 하는 메서드를 추가 했습니다. 여기 [(c](/dotnet/api/microsoft.cognitiveservices.speech) [+ +)](/cpp/cognitive-services/speech/microsoft-cognitiveservices-speech-namespace), 여기 ( [Java)](/java/api/com.microsoft.cognitiveservices.speech), 여기 ( [Python)](/python/api/azure-cognitiveservices-speech/azure.cognitiveservices.speech), 여기 ( [목적-C/Swift)](/objectivec/cognitive-services/speech/)에서 참조 설명서를 읽으십시오.
- **C #, c + +, Java**: `FromDialogServiceConnector()` `Connection` 에 대 한 연결 및 연결 끊기 이벤트를 모니터링 하는 데 사용할 수 있는 함수를 클래스에 추가 했습니다 `DialogServiceConnector` . 여기 ( [c #)](/dotnet/api/microsoft.cognitiveservices.speech.connection), 여기 ( [c + +)](/cpp/cognitive-services/speech/connection), 여기 ( [Java)](/java/api/com.microsoft.cognitiveservices.speech.connection)에서 참조 설명서를 읽으십시오.
- **C + +/c #/Java/Python/Objective-C/Swift**: 음성 발음을 평가 하 고 음성 오디오의 정확도와 능숙에 대 한 발표자 피드백을 제공 하는 발음 평가에 대 한 지원이 추가 되었습니다. [여기](how-to-pronunciation-assessment.md)에서 설명서를 참조 하세요.

**주요 변경 내용**
- **JavaScript**: PullAudioOutputStream ()에는 내부 약속에서 네이티브 JavaScript 약속으로의 반환 형식 변경 내용이 있습니다.

**버그 수정**
- **All**: `SetServiceProperty` 특정 특수 문자가 포함 된 값이 무시 된에서 1.13 회귀를 수정 했습니다.
- **C #**: Visual Studio 2019의 Windows 콘솔 샘플을 수정 하 여 네이티브 dll을 찾지 못했습니다.
- **C #**: 스트림을 입력으로 사용 하는 경우 메모리 관리의 충돌 문제를 수정 `KeywordRecognizer` 했습니다.
- **ObjectiveC/Swift**: 스트림이 인식기 입력으로 사용 되는 경우 메모리 관리와의 충돌 문제를 수정 했습니다.
- **Windows**: UWP에서 BT HFP/A2DP의 동시 존재 문제를 해결 했습니다.
- **JavaScript**: 로그를 개선 하 고 내부 디버그/서비스 상관 관계를 지원 하기 위해 세션 id 매핑을 수정 했습니다.
- **JavaScript**: `DialogServiceConnector` `ListenOnce` 첫 번째 호출을 수행한 후 호출을 사용 하지 않도록 설정 하는 수정이 추가 되었습니다.
- **JavaScript**: 결과 출력이 "simple"이 될 때까지 문제가 해결 되었습니다.
- **JavaScript**: Macos의 Safari에서 지속적인 인식 문제를 수정 했습니다.
- **JavaScript**: 높은 요청 처리량 시나리오에 대 한 CPU 로드 완화
- **JavaScript**: 음성 프로필 등록 결과의 세부 정보에 대 한 액세스를 허용 합니다.
- **JavaScript**:에서 지속적인 인식을 위한 수정이 추가 되었습니다 `IntentRecognizer` .
- **C + +/c #/Java/Python/Swift/ObjectiveC**:에서 australiaeast 및 brazilsouth에 대 한 잘못 된 url을 수정 했습니다 `IntentRecognizer` .
- **C + +/c #**: `VoiceProfileType` 개체를 만들 때 인수로 추가 `VoiceProfile` 됩니다.
- **C + +/c #/Java/Python/Swift/ObjectiveC**: `SPX_INVALID_ARG` `AudioDataStream` 지정 된 위치에서 읽으려고 할 때 발생할 수 있는 문제를 수정 했습니다.
- **IOS**: Unity에서 음성 인식이 충돌 하는 문제 해결

**샘플**
- **ObjectiveC**: [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/objective-c/ios/speech-samples)에 키워드 인식을 위한 샘플이 추가 되었습니다.
- **C #/Javascript**: 여기에서 대화에 대 한 빠른 시작 [(c #)](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/csharp/dotnet/conversation-transcription) 및 [여기 (JavaScript)](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/javascript/node/conversation-transcription)가 추가 되었습니다.
- **C + +/c #/Java/Python/Swift/ObjectiveC**: [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples) 에 발음 평가를 위한 샘플이 추가 되었습니다.
- **Xamarin**: [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/csharp/xamarin)에서 최신 Visual Studio 템플릿에 대 한 빠른 시작을 업데이트 했습니다.

**알려진 문제**
- DigiCert 전역 루트 G2 인증서는 HoloLens 2 및 Android 4.4 (KitKat)에서 기본적으로 지원 되지 않으며, 음성 SDK 기능을 수행 하기 위해 시스템에 추가 해야 합니다. 이 인증서는 곧 HoloLens 2 OS 이미지에 추가 됩니다. Android 4.4 고객은 업데이트 된 인증서를 시스템에 추가 해야 합니다.

**Covid-19 요약 테스트:** 지난 몇 주 동안 원격으로 작업 하기 때문에 일반적으로 수행 하는 것 처럼 많은 수동 확인 테스트를 수행할 수 없습니다. 모든 항목을 손상 했을 수 있으며 자동화 된 테스트가 모두 통과 했을 수 있습니다. 오류가 발생 하지 않은 경우 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen)에서 알려주세요.<br>
정상 상태를 유지 하세요.

## <a name="speech-cli-also-known-as-spx-2020-october-release"></a>Speech CLI (SPX 라고도 함): 2020-10 월 릴리스
SPX는 코드를 작성 하지 않고 Azure Speech service를 사용 하는 명령줄 인터페이스입니다. [여기](./spx-basics.md)에서 최신 버전을 다운로드 하세요. <br>

**새로운 기능**
- `spx csr dataset upload --kind audio|language|acoustic` – Url 뿐만 아니라 로컬 데이터에서 데이터 집합을 만듭니다.
- `spx csr evaluation create|status|list|update|delete` – 새 모델을 기준 진위/기타 모델과 비교 합니다.
- `spx * list` – 페이지가 아닌 환경을 지원 합니다 (--top X--skip X가 필요 하지 않음).
- `spx * --http header A=B` – 사용자 지정 헤더를 지원 합니다 (사용자 지정 인증을 위해 Office에 추가 됨). 
- `spx help` – 향상 된 텍스트 및 배경 텍스트 색 (파란색)

## <a name="text-to-speech-2020-september-release"></a>텍스트 음성 변환 2020-9 월 릴리스

### <a name="new-features"></a>새로운 기능

* **신경망** 
    * **18 개의 새로운 언어/로캘을 지원 하도록 확장 되었습니다.** 불가리아어, 체코어, 독일어 (오스트리아), 독일어 (스위스), 그리스어, 영어 (아일랜드), 프랑스어 (스위스), 히브리어, 크로아티아어, 헝가리어, 인도네시아어, 말레이어, 루마니아어, 슬로바키아어, 슬로베니아어, 타밀어, 텔루구어 및 베트남어입니다. 
    * **14 개의 새 음성을 출시 하 여 기존 언어의 다양 한를 보강 합니다.** [전체 언어 및 음성 목록을](language-support.md#neural-voices)참조 하세요.
    * **및 음성의 새로운 말하는 스타일 `en-US` `zh-CN` .** 영어 (미국)로 된 새 음성은의 봇, 고객 서비스 및 보조자 스타일을 지원 합니다. 10 개의 새로운 말하는 스타일은 zh-cn 음성, XiaoXiao에서 사용할 수 있습니다. 또한 XiaoXiao 신경망은 조정을 지원 합니다 `StyleDegree` . [SSML에서 말하는 스타일을 사용 하는 방법을](speech-synthesis-markup.md#adjust-speaking-styles)참조 하세요.

* **컨테이너: 공개 미리 보기에서 릴리스된 신경망은 14 개 언어로 제공 되는 16 개의 음성을 제공 합니다.** [신경망에 대해 음성 컨테이너를 배포 하는 방법](speech-container-howto.md) 에 대 한 자세한 정보  

[Ignite 2020에 대 한 TTS 업데이트에 대 한 전체 공지](https://techcommunity.microsoft.com/t5/azure-ai/ignite-2020-neural-tts-updates-new-language-support-more-voices/ba-p/1698544) 를 읽으십시오. 

## <a name="text-to-speech-2020-august-release"></a>텍스트 음성 변환 2020-8 월 릴리스

### <a name="new-features"></a>새로운 기능

* **신경망: 새 말하기 스타일 `en-US` Aria 음성**. 뉴스는 뉴스를 읽을 때 AriaNeural 수 있습니다. ' Newscast-공식 ' 스타일은 더 심각 하 게 들리지만 ' newscast-일반 ' 스타일은 더 낮은 수준에서 비공식적입니다. [SSML에서 말하는 스타일을 사용 하는 방법을](speech-synthesis-markup.md)참조 하세요.

* **사용자 지정 음성: 학습 데이터 품질을 자동으로 확인 하기 위해 새로운 기능이 출시 되었습니다**. 데이터를 업로드 하면 시스템에서 오디오 및 성적 데이터의 다양 한 측면을 검사 하 고, 음성 모델의 품질을 향상 시키기 위해 문제를 자동으로 해결 하거나 필터링 합니다. 오디오 및 스크립트 형식 외에도 오디오의 볼륨, 노이즈 수준, 음성의 발음 정확도, 표준화 된 텍스트가 있는 음성 맞춤, 오디오의 무음 등을 다룹니다. 

* **오디오 콘텐츠 생성: 강력한 음성 조정 및 오디오 관리 기능을 제공 하는 새로운 기능 집합** 입니다.

    * 발음: 음성 조정 기능이 최신 음소 집합으로 업데이트 됩니다. 라이브러리에서 right 음소 요소를 선택 하 고 선택한 단어의 발음을 구체화할 수 있습니다. 

    * 다운로드: 단락에서 오디오 생성을 지원 하도록 오디오 "다운로드"/"내보내기" 기능이 향상 되었습니다. 여러 오디오 출력을 생성 하는 동안 동일한 파일/SSML에서 콘텐츠를 편집할 수 있습니다. "다운로드"의 파일 구조도 구체화 됩니다. 이제 한 폴더의 모든 오디오 파일을 쉽게 가져올 수 있습니다. 

    * 작업 상태: 다중 파일 내보내기 환경이 개선 되었습니다. 과거에 여러 파일을 내보낼 때 파일 중 하나가 실패 하면 전체 작업이 실패 합니다. 그러나 이제 다른 모든 파일은 성공적으로 내보내집니다. 작업 보고서는 보다 상세 하 고 구조화 된 정보로 보강 됩니다. 이제 보고서를 사용 하 여 실패 한 모든 파일 및 문장의 로그를 확인할 수 있습니다. 

    * SSML 설명서: 모든 튜닝 기능을 사용 하는 방법에 대 한 규칙을 확인 하는 데 도움이 되는 SSML 문서에 연결 됩니다.

* **음성 목록 API는 사용자에 게 친숙 한 표시 이름과 신경망에 대해 지원 되는 말하는 스타일을 포함 하도록 업데이트 됩니다**.

### <a name="general-tts-voice-quality-improvements"></a>일반 TTS 음성 품질 향상

* 단어 수준 발음 오류% 감소 `ru-RU` (오류 56% 감소) 및 `sv-SE` (오류 49% 감소)

* 신경망에서 polyphony 단어가 `en-US` 40%까지 향상 되었습니다. Polyphony 단어의 예로는 "읽기", "라이브", "콘텐츠", "레코드", "개체" 등이 있습니다. 

* 에서 발신음의 naturalness 향상 `fr-FR` 되었습니다. MOS (평균 의견 점수) 이득: + 0.28

* Vocoders는 다음과 같은 음성에 대해 향상 된 기능 및 전반적인 성능 속도를 40%로 업데이트 했습니다.

    | Locale | 음성 |
    |---|---|    
    | `en-GB` | Mia |
    | `es-MX` | Dalia |
    | `fr-CA` | Sylvie |
    | `fr-FR` | Denise |
    | `ja-JP` | Nanami |
    | `ko-KR` | Sun-Hi |

### <a name="bug-fixes"></a>버그 수정

* 오디오 콘텐츠 생성 도구를 사용 하 여 많은 버그 수정 
    * 자동 새로 고침 문제를 해결 했습니다. 
    * 남부 동아시아 지역에서 zh-cn의 음성 스타일 문제를 수정 했습니다.
    * ' Break ' 태그가 있는 내보내기 오류와 구두점 오류가 포함 된 안정성 문제가 수정 되었습니다.

## <a name="new-speech-to-text-locales-2020-august-release"></a>새 음성 텍스트 로캘: 2020-8 월 릴리스
8 월에는 음성 텍스트에서 26 개의 새 로캘이 출시 되었습니다. 2 유럽 언어 `cs-CZ` 와 `hu-HU` , 영어 (미국) 로캘, 영어 (미국)를 포함 하는 스페인어 로캘이 모두 포함 됩니다. 다음은 새 로캘의 목록입니다. [여기](./language-support.md)에서 전체 언어 목록을 참조 하세요.

| Locale  | 언어                          |
|---------|-----------------------------------|
| `cs-CZ` | 체코어(체코)            | 
| `en-HK` | 영어 (홍콩)               | 
| `en-IE` | 영어(아일랜드)                 | 
| `en-PH` | 영어(필리핀)             | 
| `en-SG` | 영어(싱가포르)               | 
| `en-ZA` | 영어(남아프리카 공화국)            | 
| `es-AR` | 스페인어(아르헨티나)               | 
| `es-BO` | 스페인어(볼리비아)                 | 
| `es-CL` | 스페인어(칠레)                   | 
| `es-CO` | 스페인어(콜롬비아)                | 
| `es-CR` | 스페인어(코스타리카)              | 
| `es-CU` | 스페인어 (쿠바)                    | 
| `es-DO` | 스페인어(도미니카 공화국)      | 
| `es-EC` | 스페인어(에콰도르)                 | 
| `es-GT` | 스페인어(과테말라)               | 
| `es-HN` | 스페인어(온두라스)                | 
| `es-NI` | 스페인어(니카라과)               | 
| `es-PA` | 스페인어(파나마)                  | 
| `es-PE` | 스페인어(페루)                    | 
| `es-PR` | 스페인어(푸에르토리코)             | 
| `es-PY` | 스페인어(파라과이)                | 
| `es-SV` | 스페인어(엘살바도르)             | 
| `es-US` | 스페인어 (미국)                     | 
| `es-UY` | 스페인어(우루과이)                 | 
| `es-VE` | 스페인어(베네수엘라)               | 
| `hu-HU` | 헝가리어(헝가리)               | 


## <a name="speech-sdk-1130-2020-july-release"></a>Speech SDK 1.13.0:2020-7 월 릴리스

**참고**: Windows의 Speech SDK는 Visual Studio 2015, 2017 및 2019에 대 한 공유 Microsoft Visual C++ 재배포 가능 패키지에 따라 달라 집니다. [여기](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)에서 다운로드하여 설치합니다.

**새로운 기능**
- **C #**: 비동기 대화 기록을 위한 지원이 추가 되었습니다. [여기](./how-to-async-conversation-transcription.md)에서 설명서를 참조 하세요.  
- **JavaScript**: [브라우저](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/javascript/browser/speaker-recognition) 와 [node.js](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/javascript/node/speaker-recognition)에 대 한 Speaker Recognition 지원이 추가 되었습니다.
- **JavaScript**: 자동 언어 검색/언어 ID에 대 한 지원이 추가 되었습니다. [여기](./how-to-automatic-language-detection.md?pivots=programming-language-javascript)에서 설명서를 참조 하세요.
- **목적-C**: [다중 장치 대화](./multi-device-conversation.md) 및 [대화](./conversation-transcription.md)기록에 대 한 지원이 추가 되었습니다. 
- **Python**: Windows 및 Linux에서 python에 대 한 압축 오디오 지원을 추가 했습니다. [여기](./how-to-use-codec-compressed-audio-input-streams.md)에서 설명서를 참조 하세요. 

**버그 수정**
- **모두**: 인식 후 KeywordRecognizer 스트림을 앞으로 이동 하지 않는 문제를 해결 했습니다.
- **All**: KeywordRecognitionResult에서 가져온 스트림이 키워드를 포함 하지 않도록 하는 문제를 해결 했습니다.
- **모든**: 사용자가 대기를 완료 한 후 SendMessageAsync가 네트워크를 통해 메시지를 전송 하지 않는 문제를 해결 했습니다.
- **모든**: 사용자가 VoiceProfileClient:: SpeakerRecEnrollProfileAsync 메서드를 여러 번 호출 하 고 호출이 완료 될 때까지 기다리지 않는 경우 Speaker Recognition api에서 충돌이 해결 되었습니다.
- **All**: VoiceProfileClient 및 SpeakerRecognizer 클래스에서 파일 로깅 사용을 수정 했습니다.
- **JavaScript**: 브라우저가 최소화 되었을 때 조정 [문제](https://github.com/microsoft/cognitive-services-speech-sdk-js/issues/74) 를 수정 했습니다.
- **JavaScript**: 스트림에서 메모리 누수가 발생 한 [문제](https://github.com/microsoft/cognitive-services-speech-sdk-js/issues/78) 를 수정 했습니다.
- **JavaScript**: nodejs에서 OCSP 응답에 대 한 캐싱을 추가 했습니다.
- **Java**: BigInteger 필드에서 항상 0을 반환 하는 문제를 해결 했습니다.
- **ios**: Ios 앱 스토어에서 음성 SDK 기반 앱을 게시 하는 [문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/702) 를 해결 했습니다.

**샘플**
- **C + +**: [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/cpp/windows/console/samples/speaker_recognition_samples.cpp)에 Speaker Recognition 샘플 코드를 추가 했습니다.

**Covid-19 요약 테스트:** 지난 몇 주 동안 원격으로 작업 하기 때문에 일반적으로 수행 하는 것 처럼 많은 수동 확인 테스트를 수행할 수 없습니다. 모든 항목을 손상 했을 수 있으며 자동화 된 테스트가 모두 통과 했을 수 있습니다. 오류가 발생 하지 않은 경우 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen)에서 알려주세요.<br>
정상 상태를 유지 하세요.

## <a name="text-to-speech-2020-july-release"></a>텍스트 음성 변환 2020-7 월 릴리스

### <a name="new-features"></a>새로운 기능

* **신경망, 15 개의 새로운 신경망**: 신경망에 추가 된 새 음성: 신경망 `ar-EG` (이집트), Zariyah (아랍어), Salma `ar-SA` `ca-ES` (스페인), 카탈로니아어 (스페인), Christel `da-DK` (덴마크), Neerja ( `es-IN` 영어 (인도)) Noora `fi-FI` (핀란드), 힌디어 (인도), Swara의 `hi-IN` Colette, 네덜란드어 (네덜란드), 폴란드어 (폴란드어) `nl-NL` `pl-PL` `pt-PT` `ru-RU` `sv-SE` `th-TH` `zh-HK` `zh-TW` , Fernanda In 러시아어 (폴란드어), Dariya in 러시아어 (러시아), Hillevi in 태국어 (태국), Achara in 스웨덴어 (HiuGaai, 번체) 및 광둥어 in 중국어 (HsiaoYu 대만) [지원 되](./language-support.md#neural-voices)는 모든 언어를 확인 합니다.  

* **사용자 환경을 단순화 하기 위해 학습 흐름을 사용한 사용자 지정 음성, 간소화 된 음성 테스트**: 새로운 테스트 기능을 사용 하면 각 음성이 일반 및 음성 도우미 시나리오를 다루는 각 언어에 대해 최적화 된 미리 정의 된 테스트 집합으로 자동으로 테스트 됩니다. 이러한 테스트 집합은 신중 하 게 선택 하 고 테스트 하 여 일반적인 사용 사례와 언어의 음소을 포함 합니다. 뿐만 아니라 사용자가 모델을 학습할 때 자체 테스트 스크립트를 업로드 하도록 선택할 수 있습니다.

* **오디오 콘텐츠 만들기: 강력한 음성 조정 및 오디오 관리 기능을 지원 하기 위해 새로운 기능 집합이 릴리스 되었습니다.**

    * `Pitch`, `rate` 및 `volume` 는 속도가 느리고 medium 및 fast와 같은 미리 정의 된 값을 사용 하 여 조정을 지원 하도록 향상 되었습니다. 이제 사용자는 오디오 편집을 위해 ' 상수 ' 값을 쉽게 선택할 수 있습니다.

    ![오디오 튜닝](media/release-notes/audio-tuning.png)

    * 이제 사용자는 `Audio history` 작업 파일에 대 한을 검토할 수 있습니다. 이 기능을 사용 하면 사용자가 작업 파일과 관련 하 여 생성 된 모든 오디오를 쉽게 추적할 수 있습니다. 기록 버전을 확인 하 고 동시에 조정 하는 동안 품질을 비교할 수 있습니다. 

    ![오디오 기록](media/release-notes/audio-history.png)

    * `Clear`이제 기능이 더욱 유연 합니다. 사용자는 선택한 콘텐츠에 사용할 수 있는 다른 매개 변수를 유지 하면서 특정 튜닝 매개 변수를 지울 수 있습니다.  

    * 사용자가 TTS 음성 조정 및 오디오 관리를 신속 하 게 시작 하는 데 도움이 되는 자습서 비디오가 [방문 페이지](https://speech.microsoft.com/audiocontentcreation) 에 추가 되었습니다. 

### <a name="general-tts-voice-quality-improvements"></a>일반 TTS 음성 품질 향상

* 더 높은 충실도 및 짧은 대기 시간을 위해에서 TTS vocoder 향상 되었습니다.

    * Elsa를 `it-IT` 새로운 vocoder로 업데이트 했습니다 .이는 + 0.464 CMOS (비교 평균 인)에 게 음성 품질, 40% 더 빠른 통합 및 30%의 첫 번째 바이트 대기 시간을 얻습니다. 
    * `zh-CN`일반 도메인에 대해 + 0148 CMOS를 사용 하 고, newscast 스타일의 경우 + 0.348, lyrical 스타일의 경우 + 0.195로 Xiaoxiao을 새 vocoder로 업데이트 했습니다. 

* `de-DE` `ja-JP` TTS 출력 보다 자연스럽 게 보이도록 업데이트 된 및 음성 모델
    
    * `de-DE`최신 prosody 모델링 방법으로 Katja이 업데이트 되었습니다. MOS (평균 의견 점수) 이득은 + 0.13입니다. 
    * `ja-JP`새 피치 강조 prosody 모델을 사용 하 여 Nanami을 업데이트 했습니다. MOS (평균 인지 점수) 이득은 + 0.19입니다.  

* 5 개 언어로 된 단어 수준 음성 정확도 향상

    | 언어 | 음성 오류 감소 |
    |---|---|
    | `en-GB` | 51% |
    | `ko-KR` | 17% |
    | `pt-BR` | 39% |
    | `pt-PT` | 77% |
    | `id-ID` | 46% |

### <a name="bug-fixes"></a>버그 수정

* 통화 판독값
    * 및에 대 한 통화 읽기와 관련 된 문제를 해결 했습니다. `es-ES``es-MX`
     
    | 언어 | 입력 | 개선 후의 기능 |
    |---|---|---|
    | `es-MX` | $1.58 | un 페소 cincuenta y ocho centavos |
    | `es-ES` | $1.58 | un dólar cincuenta y ocho centavos |

    * ,,,,, 로캘에서 음수 통화 (예: "-€325")를 지원 `en-US` `en-GB` `fr-FR` `it-IT` `en-AU` `en-CA` 합니다.

* 에서 주소 읽기가 개선 `pt-PT` 되었습니다.
* `en-AU` `en-UK` "For" 및 "4" 단어에 대 한 Natasha () 및 수정 ()의 발음 문제를 수정 했습니다.  
* 오디오 콘텐츠 생성 도구에 대 한 버그 수정 됨
    * 두 번째 단락 뒤의 추가 및 예기치 않은 일시 중지가 수정 되었습니다.  
    * 회귀 버그에서 ' 중단 없음 ' 기능이 다시 추가 됩니다. 
    * Speech Studio의 무작위 새로 고침 문제는 고정 되어 있습니다.  

### <a name="samplessdk"></a>샘플/SDK

* JavaScript: Firefox 및 macOS 및 iOS의 Safari에서 재생 문제를 수정 합니다. 

## <a name="speech-sdk-1121-2020-june-release"></a>Speech SDK 1.12.1:2020-6 월 릴리스
**Speech CLI (SPX 라고도 함)**
-   CLI 내 도움말 검색 기능이 추가 되었습니다.
    -   `spx help find --text TEXT`
    -   `spx help find --topic NAME`
-   새로 배포 된 v 3.0 Batch 및 Custom Speech Api와 함께 작동 하도록 업데이트 되었습니다.
    -   `spx help batch examples`
    -   `spx help csr examples`

**새로운 기능**
-   **C \# , c + +**: Speaker Recognition 미리 보기:이 기능을 사용 하면 발표자 식별 (말하는 사람) 및 스피커 확인 (해당 하는 스피커가 무엇 인가요?)이 가능 합니다. [개요](./speaker-recognition-overview.md)부터 시작 하 여 [Speaker Recognition 기본 문서](./get-started-speaker-recognition.md)또는 [API 참조](/rest/api/speakerrecognition/)문서를 참고 하세요.

**버그 수정**
-   **C \# , c + +**: 고정 마이크 기록이 스피커 인식에서 1.12에서 작동 하지 않았습니다.
-   **JavaScript**: Firefox에서 텍스트 음성 변환 및 Macos 및 IOS의 Safari를 수정 합니다.
-   8 채널 스트림을 사용 하는 경우 대화에 대 한 Windows 응용 프로그램 검증 도구 검증 액세스 위반 충돌을 수정 합니다.
-   다중 장치 대화 변환에서 Windows 응용 프로그램 검증 도구 액세스 위반 충돌을 수정 합니다.

**샘플**
-   **C #**: 스피커 인식을 위한 [코드 샘플](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/csharp/dotnet/speaker-recognition) 입니다.
-   **C + +**: 스피커 인식을 위한 [코드 샘플](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/cpp/windows/speaker-recognition) 입니다.
-   **Java**: Android의 의도 인식에 대 한 [코드 샘플](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/java/android/intent-recognition) 입니다. 

**Covid-19 요약 테스트:** 지난 몇 주 동안 원격으로 작업 하기 때문에 일반적으로 수행 하는 것 처럼 많은 수동 확인 테스트를 수행할 수 없습니다. 모든 항목을 손상 했을 수 있으며 자동화 된 테스트가 모두 통과 했을 수 있습니다. 오류가 발생 하지 않은 경우 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen)에서 알려주세요.<br>
정상 상태를 유지 하세요.


## <a name="speech-sdk-1120-2020-may-release"></a>Speech SDK 1.12.0:2020-릴리스 수
**음성 CLI (SPX로도 인식)**
- **SPX** 는 명령줄에서 인식, 합성, 번역, 배치 기록 및 사용자 지정 음성 관리를 수행할 수 있도록 하는 새로운 명령줄 도구입니다. 이를 사용 하 여 음성 서비스를 테스트 하거나 수행 해야 하는 음성 서비스 작업을 스크립팅할 수 있습니다. 도구를 다운로드 하 고 [여기](./spx-overview.md)에서 설명서를 읽으십시오.

**새로운 기능**
- **Go**: [음성 인식](./get-started-speech-to-text.md?pivots=programming-language-go) 및 [사용자 지정 음성 도우미](./quickstarts/voice-assistants.md?pivots=programming-language-go)에 대 한 새로운 go 언어 지원. [여기](./quickstarts/setup-platform.md?pivots=programming-language-go)에서 개발 환경을 설정 합니다. 샘플 코드는 아래의 샘플 섹션을 참조 하세요. 
- **JavaScript**: 텍스트 음성 변환에 대 한 브라우저 지원이 추가 되었습니다. [여기](./get-started-text-to-speech.md?pivots=programming-language-JavaScript)에서 설명서를 참조 하세요.
- **C + +, c #, Java**: `KeywordRecognizer` Windows, Android, Linux & iOS 플랫폼에서 지원 되는 새 개체 및 api. [여기](./custom-keyword-overview.md)에서 설명서를 참조 하세요. 샘플 코드는 아래의 샘플 섹션을 참조 하세요. 
- **Java**: 번역 지원이 포함 된 다중 장치 대화를 추가 했습니다. 참조 문서는 [여기](/java/api/com.microsoft.cognitiveservices.speech.transcription)를 참조 하세요.

**& 최적화 기능 향상**
- **JavaScript**: 최적화 된 브라우저 마이크 구현 음성 인식 정확도 향상.
- **Java**: SWIG 없이 direct JNI 구현을 사용 하 여 바인딩을 리팩터링 했습니다. 이 변경은 Windows, Android, Linux 및 Mac에 사용 되는 모든 Java 패키지에 대 한 바인딩 크기를 10 배 하 고, 음성 SDK Java 구현에 대 한 추가 개발을 용이 하 게 합니다.
- **Linux**: 최신 RHEL 7 관련 정보를 사용 하 여 지원 [설명서](./speech-sdk.md?tabs=linux) 를 업데이트 했습니다.
- 서비스 및 네트워크 오류가 발생할 때 여러 번 연결을 시도 하는 연결 논리가 개선 되었습니다.
- 개발자가 Azure Speech portal.azure.com의 다음 단계를 수행 하는 데 도움이 되는 [](https://portal.azure.com) Speech 빠른 시작 페이지가 업데이트 되었습니다.

**버그 수정**
- **C #, Java**: Linux ARM (32 비트 및 64 비트 모두)에서 SDK 라이브러리를 로드 하는 [문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/587) 를 해결 했습니다.
- **C #**: TranslationRecognizer, IntentRecognizer 및 연결 개체에 대 한 네이티브 핸들의 명시적 삭제를 수정 했습니다.
- **C #**: ConversationTranscriber 개체에 대 한 오디오 입력 수명 관리를 수정 했습니다.
- `IntentRecognizer`간단한 구의 의도를 인식할 때 결과 이유가 올바르게 설정 되지 않은 문제를 해결 했습니다.
- `SpeechRecognitionEventArgs`결과 오프셋이 올바르게 설정 되지 않은 문제를 해결 했습니다.
- Websocket 연결을 열기 전에 SDK에서 네트워크 메시지를 보내려고 시도 하는 경합 상태를 수정 했습니다. `TranslationRecognizer`참가자를 추가 하는 동안를 재현할 때
- 키워드 인식기 엔진의 메모리 누수 문제를 수정 했습니다.

**샘플**
- **Go**: [음성 인식](./get-started-speech-to-text.md?pivots=programming-language-go) 및 [사용자 지정 음성 도우미](./quickstarts/voice-assistants.md?pivots=programming-language-go)에 대 한 빠른 시작을 추가 했습니다. [여기](https://github.com/microsoft/cognitive-services-speech-sdk-go/tree/master/samples)에서 샘플 코드를 찾습니다. 
- **JavaScript**: [텍스트 음성](./get-started-text-to-speech.md?pivots=programming-language-javascript)변환, [변환](./get-started-speech-translation.md?pivots=programming-language-csharp&tabs=script)및 [의도 인식](./quickstarts/intent-recognition.md?pivots=programming-language-javascript)에 대 한 빠른 시작을 추가 했습니다.
- [C \# ](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/csharp/uwp/keyword-recognizer) 및 [Java](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/java/android/keyword-recognizer) 에 대 한 키워드 인식 샘플 (Android).  

**Covid-19 요약 테스트:** 지난 몇 주 동안 원격으로 작업 하기 때문에 일반적으로 수행 하는 것 처럼 많은 수동 확인 테스트를 수행할 수 없습니다. 모든 항목을 손상 했을 수 있으며 자동화 된 테스트가 모두 통과 했을 수 있습니다. 누락 된 내용이 있으면 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen)에서 알려주세요.<br>
정상 상태를 유지 하세요.

## <a name="speech-sdk-1110-2020-march-release"></a>Speech SDK 1.11.0:2020-3 월 릴리스
**새로운 기능**
- Linux: Speech SDK 용 시스템을 구성 하는 방법에 대 한 [지침](./how-to-configure-rhel-centos-7.md) 과 함께 RED HAT ENTERPRISE LINUX (RHEL)/CentOS 7 x64에 대 한 지원이 추가 되었습니다.
- Linux: Linux ARM32 및 ARM64의 .NET Core c #에 대 한 지원이 추가 되었습니다. 자세한 내용은 [여기](./speech-sdk.md?tabs=linux)를 읽어보세요. 
- C #, c + +: `UtteranceId` `ConversationTranscriptionResult` 모든 intermediates 및 최종 음성 인식 결과에서 일관 된 ID를에 추가 했습니다. [C #](/dotnet/api/microsoft.cognitiveservices.speech.transcription.conversationtranscriptionresult), [c + +](/cpp/cognitive-services/speech/transcription-conversationtranscriptionresult)에 대 한 세부 정보입니다.
- Python:에 대 한 지원이 추가 되었습니다 `Language ID` . [GitHub 리포지토리의](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/python/console)speech_sample py를 참조 하세요.
- Windows: 모든 win32 콘솔 응용 프로그램에 대해 Windows 플랫폼에서 압축 된 오디오 입력 형식 지원을 추가 했습니다. 자세한 내용은 [여기](./how-to-use-codec-compressed-audio-input-streams.md)를 참조 하세요. 
- JavaScript: NodeJS에서 음성 합성 (텍스트-음성)을 지원 합니다. [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/javascript/node/text-to-speech)를 참조하세요. 
- JavaScript: 모든 송신 및 수신 메시지를 검사할 수 있도록 새 API를 추가 합니다. [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/javascript)를 참조하세요. 
        
**버그 수정**
- C #, c + +: `SendMessageAsync` 이제 이진 메시지를 이진 형식으로 전송 하는 문제가 해결 되었습니다. [C #](/dotnet/api/microsoft.cognitiveservices.speech.connection.sendmessageasync#Microsoft_CognitiveServices_Speech_Connection_SendMessageAsync_System_String_System_Byte___System_UInt32_), [c + +](/cpp/cognitive-services/speech/connection)에 대 한 세부 정보입니다.
- C #, c + +: `Connection MessageReceived` `Recognizer` 개체가 이전에 삭제 된 경우 이벤트를 사용 하 여 충돌이 발생할 수 있는 문제를 해결 함. `Connection` [C #](/dotnet/api/microsoft.cognitiveservices.speech.connection.messagereceived), [c + +](/cpp/cognitive-services/speech/connection#messagereceived)에 대 한 세부 정보입니다.
- Android: 대기 시간을 개선 하기 위해 마이크의 오디오 버퍼 크기를 800ms에서 100ms로 줄였습니다.
- Android: Android Studio의 x86 Android emulator [문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/563) 를 해결 했습니다.
- JavaScript: API를 사용 하 여 중국의 지역에 대 한 지원이 추가 되었습니다 `fromSubscription` . 자세한 내용은 [여기](/javascript/api/microsoft-cognitiveservices-speech-sdk/speechconfig#fromsubscription-string--string-)를 참조 하세요. 
- JavaScript: NodeJS의 연결 실패에 대 한 오류 정보를 추가 합니다.
        
**샘플**
- Unity: LUIS json 가져오기가 실패 한 경우에 의도 인식 public 샘플이 고정 되어 있습니다. 자세한 내용은 [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/369)를 참조 하세요.
- Python:에 대 한 샘플이 추가 되었습니다 `Language ID` . 자세한 내용은 [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/samples/python/console/speech_sample.py)를 참조 하세요.
    
**Covid19 요약 테스트:** 지난 몇 주 동안 원격으로 작업 하기 때문에 일반적으로 수행 하는 것 처럼 많은 수동 장치 확인 테스트를 수행할 수 없습니다. 예를 들어 Linux, iOS 및 macOS에서 마이크 입력 및 스피커 출력을 테스트할 수 없습니다. 이러한 플랫폼의 모든 항목을 손상 했을 수 있는 것으로 생각 하 고 자동화 된 테스트를 모두 통과 한 것은 아닙니다. 오류가 발생 하지 않은 경우 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen)에서 알려주세요.<br> 계속 지원 해 주셔서 감사 합니다. 언제 든 지 [GitHub](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues?q=is%3Aissue+is%3Aopen) 또는 [Stack Overflow](https://stackoverflow.microsoft.com/questions/tagged/731)에 대 한 질문이 나 의견을 게시 해 주시기 바랍니다.<br>
정상 상태를 유지 하세요.

## <a name="speech-sdk-1100-2020-february-release"></a>Speech SDK 1.10.0:2020-2 월 릴리스

**새로운 기능**

 - Python의 새로운 3.8 릴리스를 지 원하는 Python 패키지를 추가 했습니다.
 - Red Hat Enterprise Linux (RHEL)/CentOS 8 x64 지원 (c + +, c #, Java, Python).
   > [!NOTE] 
   > 고객은 [이러한 지침](./how-to-configure-openssl-linux.md)에 따라 OpenSSL를 구성 해야 합니다.
 - Debian 및 Ubuntu에 대 한 Linux ARM32 지원.
 - DialogServiceConnector는 이제 BotFrameworkConfig에서 선택적 "bot ID" 매개 변수를 지원 합니다. 이 매개 변수를 사용 하면 단일 Azure 음성 리소스에서 여러 개의 직접 라인 음성 봇을 사용할 수 있습니다. 매개 변수를 지정 하지 않으면 기본 봇 (직접 선 음성 채널 구성 페이지에 의해 결정 됨)이 사용 됩니다.
 - DialogServiceConnector에는 이제 SpeechActivityTemplate 속성이 있습니다. 이 JSON 문자열의 내용은 음성 인식과 같은 이벤트에 대 한 응답으로 자동으로 생성 되는 활동을 포함 하 여 직접 라인 음성 봇에 도달 하는 모든 활동에서 다양 한 지원 필드를 미리 채우도록 사용 됩니다.
 - 이제 TTS는 인증에 구독 키를 사용 하 여 신시사이저를 만든 후 첫 번째 합성 결과의 첫 번째 바이트 대기 시간을 줄입니다.
 - 18.6%의 평균 단어 오류 비율 절감을 위해 19 개 로캘에 대 한 음성 인식 모델 업데이트 (es, es-MX, fr-fr, fr-fr, it-zh-cn, ko-kr, ko-kr, pt-BR,, zh-cn-HK, nb,, fi,, pl,, zh-cn,,,)를 차례로 찾을 수 있습니다 .이에 대 한 자세한 내용은 새 모델은 받아쓰기, Call-Center 기록 및 비디오 인덱싱 시나리오를 비롯 한 여러 도메인에서 상당한 개선을 가져옵니다.

**버그 수정**

 - JAVA Api에서 대화 Transcriber 올바르게 기다리지 않는 버그가 수정 되었습니다. 
 - Xamarin [GitHub 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/363) 에 대 한 Android x86 에뮬레이터 수정
 - Missing 추가 (Get | 속성 메서드를 기타 구성으로 설정 합니다.
 - 연결이 실패할 때 audioDataStream를 중지할 수 없는 TTS 버그를 수정 합니다.
 - 지역이 없는 끝점을 사용 하면 대화 변환기에 대 한 USP 오류가 발생 합니다.
 - 유니버설 Windows 응용 프로그램의 ID 생성은 이제 적절 한 고유 GUID 알고리즘을 사용 합니다. 이전에는 대부분의 상호 작용에 대 한 충돌을 자주 생성 하는 스텁 구현에 대해 이전 및 실수로 기본 설정 되었습니다.
 
 **샘플**
 
 - [Unity 마이크 및 푸시 모드 스트리밍](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/unity/from-unitymicrophone) 에서 음성 SDK를 사용 하기 위한 unity 샘플

**기타 변경 내용**

 - [Linux 용으로 업데이트 된 OpenSSL 구성 설명서](./how-to-configure-openssl-linux.md)

## <a name="speech-sdk-190-2020-january-release"></a>Speech SDK 1.9.0:2020-1 월 릴리스

**새 기능**

- 다중 장치 대화: 동일한 음성 또는 텍스트 기반 대화에 여러 장치를 연결 하 고 필요에 따라 전송 되는 메시지를 변환 합니다. [이 문서](multi-device-conversation.md)에서 자세히 알아보세요. 
- Aar 패키지에 대 한 키워드 인식 지원이 추가 되었으며 x86 및 x64 기능에 대 한 지원이 추가 되었습니다. 
- 목적-C: `SendMessage` 및 `SetMessageProperty` 메서드가 개체에 추가 되었습니다 `Connection` . [여기](/objectivec/cognitive-services/speech/spxconnection)에서 설명서를 참조 하세요.
- TTS c + + api `std::wstring` 는 이제 합성 텍스트 입력으로 지원 되므로 wstring을 SDK로 전달 하기 전에 문자열로 변환할 필요가 없습니다. 자세한 내용은 [여기](/cpp/cognitive-services/speech/speechsynthesizer#speaktextasync)를 참조하세요. 
- C #: [언어 ID](./how-to-automatic-language-detection.md?pivots=programming-language-csharp) 및 [소스 언어 구성을](./how-to-specify-source-language.md?pivots=programming-language-csharp) 이제 사용할 수 있습니다.
- JavaScript: `Connection` 음성 서비스에서 콜백으로 사용자 지정 메시지를 전달 하는 기능을 개체에 추가 했습니다 `receivedServiceMessage` .
- JavaScript: `FromHost API` 온-프레미스 컨테이너 및 소 버린 클라우드에서 쉽게 사용할 수 있도록에 대 한 지원이 추가 되었습니다. [여기](speech-container-howto.md)에서 설명서를 참조 하세요.
- JavaScript: 이제 `NODE_TLS_REJECT_UNAUTHORIZED` [orgads](https://github.com/orgads)의 기여로 감사 합니다. 자세한 내용은 [여기](https://github.com/microsoft/cognitive-services-speech-sdk-js/pull/75)를 참조하세요.

**주요 변경 내용**

- `OpenSSL` 는 버전 1.1.1 b로 업데이트 되었으며 Linux 용 Speech SDK core 라이브러리에 정적으로 연결 됩니다. 이로 인해 수신함이 `OpenSSL` 시스템의 디렉터리에 설치 되지 않은 경우에는 중단 될 수 있습니다 `/usr/lib/ssl` . 문제를 해결 하려면 Speech SDK 문서에서 [설명서](how-to-configure-openssl-linux.md) 를 확인 하세요.
- C #에 대해 반환 되는 데이터 형식을 `WordLevelTimingResult.Offset` 에서로 변경 하 여 `int` `long` `WordLevelTimingResults` 음성 데이터가 2 분 보다 오래 된 경우에 액세스할 수 있습니다.
- `PushAudioInputStream` 이제를 기반으로 하 여 `PullAudioInputStream` wav 헤더 정보를 음성 서비스에 보냅니다 `AudioStreamFormat` .이 정보는 생성 시 선택적으로 지정 됩니다. 이제 고객이 [지원 되는 오디오 입력 형식을](how-to-use-audio-input-streams.md)사용 해야 합니다. 다른 모든 형식은 최적이 아닌 인식 결과를 얻거나 다른 문제를 일으킬 수 있습니다. 

**버그 수정**

- `OpenSSL`위의 주요 변경 내용에서 업데이트를 참조 하세요. Linux 및 Java에서 간헐적인 충돌 및 성능 문제 (높은 부하 상태에서 잠금 경합)가 모두 수정 되었습니다. 
- Java: 높은 동시성 시나리오에서 개체 닫기를 개선 했습니다.
- NuGet 패키지를 재구성. `Microsoft.CognitiveServices.Speech.core.dll`Lib 폴더에서 및의 세 가지 복사본 `Microsoft.CognitiveServices.Speech.extension.kws.dll` 을 제거 하 여 NuGet 패키지를 더 작고 더 빠르게 다운로드 하 고 일부 c + + 네이티브 앱을 컴파일하는 데 필요한 헤더를 추가 했습니다.
- [여기서](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/cpp)는 빠른 시작 샘플을 수정 했습니다. Linux, macOS, Windows에서 "마이크를 찾을 수 없음" 예외를 표시 하지 않고 종료 되었습니다.
- [이 샘플과](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/csharp/uwp/speechtotext-uwp)같은 특정 코드 경로에서 긴 음성 인식이 있는 SDK 충돌 문제를 수정 했습니다.
- [이 고객 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/396)를 해결 하기 위해 Azure 웹 앱 환경에서 SDK 배포 오류가 수정 되었습니다.
- `<voice>` `<audio>` [이 고객 문제](https://github.com/Azure-Samples/cognitive-services-speech-sdk/issues/433)를 해결 하기 위해 다중 태그 또는 태그를 사용 하는 동안 TTS 오류가 수정 되었습니다. 
- SDK가 일시 중단에서 복구 될 때 TTS 401 오류가 수정 되었습니다.
- JavaScript: [euirim](https://github.com/euirim)에서 기여 하 여 오디오 데이터의 순환 가져오기를 수정 했습니다. 
- JavaScript: 1.7에 추가 된 대로 서비스 속성을 설정 하기 위한 지원이 추가 되었습니다.
- JavaScript: 연결 오류가 발생 하 여 실패 한 websocket 다시 연결 시도가 연속적으로 발생 하는 문제를 해결 했습니다.

**샘플**

- Android에 대 한 키워드 인식 샘플이 [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/java/android/sdkdemo)에 추가 되었습니다.
- [여기](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/samples/csharp/sharedcontent/console/speech_synthesis_server_scenario_sample.cs)에 서버 시나리오에 대 한 TTS 샘플이 추가 되었습니다.
- C # 및 c + +에 대 한 다중 장치 대화 퀵 스타트를 [여기](quickstarts/multi-device-conversation.md)에 추가 했습니다.

**기타 변경 내용**

- Android에서 SDK core 라이브러리 크기를 최적화 했습니다.
- 1.9.0의 SDK `int` `string` 는 대화 Transcriber의 음성 서명 버전 필드에서 및 형식을 둘 다 지원 합니다.

## <a name="speech-sdk-180-2019-november-release"></a>Speech SDK 1.8.0:2019-11 월 릴리스

**새 기능**

- `FromHost()`온-프레미스 컨테이너 및 소 버린 클라우드에서 편리 하 게 사용할 수 있도록 API를 추가 했습니다.
- 음성 인식에 대 한 자동 소스 언어 감지 추가 (Java 및 c + +)
- `SourceLanguageConfig`필요한 소스 언어를 지정 하는 데 사용 되는 음성 인식에 대 한 개체 추가 (Java 및 c + +)
- `KeywordRecognizer`NuGet 및 Unity 패키지를 통해 Windows (UWP), Android 및 iOS에 대 한 지원이 추가 되었습니다.
- 비동기 일괄 처리에서 대화 기록을 수행 하기 위해 원격 대화 Java API가 추가 되었습니다.

**주요 변경 내용**

- 대화 Transcriber 기능이 네임 스페이스에서 이동 `Microsoft.CognitiveServices.Speech.Transcription` 되었습니다.
- 대화 Transcriber 메서드의 일부는 새 클래스로 이동 됩니다 `Conversation` .
- 32 비트 (ARMv7 및 x86) iOS에 대 한 지원 삭제

**버그 수정**

- `KeywordRecognizer`유효한 음성 서비스 구독 키 없이 로컬이 사용 되는 경우 충돌 해결

**샘플**

- 용 Xamarin 샘플 `KeywordRecognizer`
- 용 Unity 샘플 `KeywordRecognizer`
- 자동 소스 언어 감지에 대 한 c + + 및 Java 샘플입니다.

## <a name="speech-sdk-170-2019-september-release"></a>Speech SDK 1.7.0:2019-9 월 릴리스

**새 기능**

- UWP (Xamarin on 유니버설 Windows 플랫폼), Android 및 iOS에 대 한 beta 지원이 추가 됨
- Unity에 대 한 iOS 지원 추가
- `Compressed`Android, iOS 및 Linux에서 형식이 alaw, Mulaw, FLAC에 대 한 입력 지원을 추가 했습니다.
- `SendMessageAsync` `Connection` 서비스에 메시지를 보내기 위해 클래스에 추가 되었습니다.
- `SetMessageProperty` `Connection` 메시지의 속성을 설정 하기 위해 클래스에 추가 되었습니다.
- Java (JRE 및 Android), Python, Swift 및 목표에 대 한 TTS 추가 된 바인딩-C
- TTS Os, iOS 및 Android에 대 한 재생 지원을 추가 했습니다.
- TTS에 대 한 "단어 경계" 정보를 추가 했습니다.

**버그 수정**

- Android 용 Unity 2019에서 IL2CPP 빌드 문제가 수정 됨
- Wav 파일 입력에서 잘못 된 헤더의 문제를 해결 했습니다.
- 일부 연결 속성에서 고유 하지 않은 Uuid와 관련 된 문제가 해결 됨
- Swift 바인딩에서 null 허용 여부 지정자에 대 한 몇 가지 경고를 수정 했습니다 (작은 코드를 변경 해야 할 수 있음).
- 네트워크 로드를 통해 websocket 연결을 비정상적 하는 버그를 수정 했습니다.
- Android에서 때때로 중복 된 임프레션 Id를 사용 하는 문제를 수정 했습니다. `DialogServiceConnector`
- 에서 발생 하는 다중 턴 상호 작용 및 오류 보고 (이벤트를 통해)의 연결 안정성이 향상 되었습니다. `Canceled``DialogServiceConnector`
- `DialogServiceConnector`세션 시작은 이제 활성 상태에서를 호출 하는 경우를 포함 하 여 이벤트를 올바르게 제공 합니다. `ListenOnceAsync()``StartKeywordRecognitionAsync()`
- 수신 중인 활동과 연결 된 충돌을 해결 했습니다. `DialogServiceConnector`

**샘플**

- Xamarin에 대 한 빠른 시작
- Linux ARM64 정보를 사용 하 여 CPP 빠른 시작 업데이트
- IOS 정보를 사용 하 여 Unity 빠른 시작 업데이트

## <a name="speech-sdk-160-2019-june-release"></a>Speech SDK 1.6.0:2019-6 월 릴리스

**샘플**

- UWP 및 Unity의 텍스트를 음성으로 변환 하기 위한 빠른 시작 샘플
- IOS의 Swift에 대 한 빠른 시작 샘플
- 음성 & 의도 인식 및 번역을 위한 Unity 샘플
- 업데이트 된 빠른 시작 샘플 `DialogServiceConnector`

**향상된 기능/변경 사항**

- 대화 상자 네임 스페이스:
  - `SpeechBotConnector`는 `DialogServiceConnector`로 이름이 변경되었습니다.
  - `BotConfig`는 `DialogServiceConfig`로 이름이 변경되었습니다.
  - `BotConfig::FromChannelSecret()` 다음으로 다시 매핑 되었습니다. `DialogServiceConfig::FromBotSecret()`
  - 이름 바꾸기 후에는 기존의 모든 Direct Line Speech 클라이언트도 계속 지원 됩니다.
- 프록시, 영구 연결을 지원 하도록 TTS REST 어댑터 업데이트
- 잘못 된 지역이 전달 되 면 오류 메시지 개선
- Swift/목표-C:
  - 향상 된 오류 보고: 오류를 발생 시킬 수 있는 메서드는 오류 처리를 위해 개체를 노출 하는 메서드와 예외를 발생 시키는 두 가지 버전으로 제공 됩니다. `NSError` Swift에는 전자가 노출 됩니다. 이렇게 변경 하려면 기존 Swift 코드를 adaptation 해야 합니다.
  - 향상 된 이벤트 처리

**버그 수정**

- TTS 용 수정: `SpeakTextAsync` 오디오가 렌더링을 완료할 때까지 기다리지 않고 나중에 반환 되는 경우
- 전체 언어 지원을 가능 하 게 하는 c #의 문자열 마샬링을 위한 수정
- 샘플에서: net461 대상 프레임 워크를 사용 하 여 핵심 라이브러리를 로드 하는 .NET core 앱 문제에 대 한 수정
- 샘플의 출력 폴더에 네이티브 라이브러리를 배포 하기 위해 가끔씩 발생 하는 문제 해결
- 안정적으로 웹 소켓을 닫는 문제 해결
- Linux에서 부하가 높은 상태에서 연결을 여는 동안 가능한 충돌 해결
- MacOS 용 framework 번들의 누락 된 메타 데이터에 대 한 수정
- Windows에서 문제 해결 `pip install --user`

## <a name="speech-sdk-151"></a>Speech SDK 1.5.1

이 릴리스는 버그 수정 릴리스 이며 네이티브/관리 SDK에만 영향을 줍니다. SDK의 JavaScript 버전에는 영향을 주지 않습니다.

**버그 수정**

- 대화 기록을 사용할 때 FromSubscription을 수정 합니다.
- 음성 도우미에 대 한 키워드 인식에서 버그를 수정 합니다.

## <a name="speech-sdk-150-2019-may-release"></a>Speech SDK 1.5.0:2019-릴리스 수

**새로운 기능**

- 이제 Windows 및 Linux에서 키워드 인식 기능을 사용할 수 있습니다. 이 기능은 모든 마이크 유형에 서 작동할 수 있지만 현재 공식 지원은 Azure Kinect 진한 하드웨어 또는 음성 장치 SDK에 있는 마이크 배열로 제한 됩니다.
- 구문 힌트 기능은 SDK를 통해 사용할 수 있습니다. 자세한 내용은 [여기](./get-started-speech-to-text.md)를 참조하세요.
- 대화 내용 기능은 SDK를 통해 사용할 수 있습니다. [여기](./conversation-transcription.md)를 참조 하세요.
- 직접 선 음성 채널을 사용 하 여 음성 도우미에 대 한 지원을 추가 합니다.

**샘플**

- 새 기능 또는 SDK에서 지 원하는 새로운 서비스에 대 한 샘플이 추가 되었습니다.

**향상된 기능/변경 사항**

- 서비스 동작 또는 서비스 결과 (예: 마스킹 및 기타)를 조정 하는 다양 한 인식기 속성이 추가 되었습니다.
- 이제 인식기를 만든 경우라도 표준 구성 속성을 통해 인식기를 구성할 수 있습니다 `FromEndpoint` .
- 목표-C: `OutputFormat` 속성이에 추가 되었습니다 `SPXSpeechConfiguration` .
- SDK는 이제 Linux 배포판으로 Debian 9를 지원 합니다.

**버그 수정**

- 발표자 리소스가 텍스트를 음성으로 너무 일찍 소멸 하는 문제를 해결 했습니다.

## <a name="speech-sdk-142"></a>Speech SDK 1.4.2

이 릴리스는 버그 수정 릴리스 이며 네이티브/관리 SDK에만 영향을 줍니다. SDK의 JavaScript 버전에는 영향을 주지 않습니다.

## <a name="speech-sdk-141"></a>Speech SDK 1.4.1

JavaScript 전용 릴리스입니다. 추가한 기능은 없습니다. 다음과 같이 수정했습니다.

- 웹 팩에서 https-프록시 에이전트를 로드 하지 못하도록 합니다.

## <a name="speech-sdk-140-2019-april-release"></a>Speech SDK 1.4.0:2019-4 월 릴리스

**새로운 기능**

- 이제 SDK는 텍스트 음성 변환 서비스를 베타 버전으로 지원 합니다. C + + 및 c #의 Windows 및 Linux 데스크톱에서 지원 됩니다. 자세한 내용은 [텍스트 음성 변환 개요](text-to-speech.md#get-started)를 참조 하세요.
- 이제 SDK는 MP3 및 Opus/OGG 오디오 파일을 스트림 입력 파일로 지원 합니다. 이 기능은 c + + 및 c #의 Linux 에서만 사용할 수 있으며 현재 베타 버전입니다 (자세한 내용은 [여기](how-to-use-codec-compressed-audio-input-streams.md)참조).
- Java, .NET core, c + + 및 목표에 대 한 음성 SDK는 macOS를 지원 합니다. MacOS에 대 한 목표-C 지원은 현재 베타 버전입니다.
- iOS: iOS 용 Speech SDK (목표-C)도 CocoaPod으로 게시 됩니다.
- JavaScript: 기본이 아닌 마이크를 입력 장치로 지원 합니다.
- JavaScript: Node.js에 대 한 프록시 지원.

**샘플**

- C + +에서 음성 SDK를 사용 하 고 macOS에서 목표-C를 사용 하는 샘플이 추가 되었습니다.
- 텍스트 음성 변환 서비스의 사용을 보여 주는 샘플이 추가 되었습니다.

**향상된 기능/변경 사항**

- Python: 이제 속성을 통해 인식 결과의 추가 속성이 노출 됩니다 `properties` .
- 추가 개발 및 디버그 지원을 위해 SDK 로깅 및 진단 정보를 로그 파일로 리디렉션할 수 있습니다 (자세한 내용은 [여기](how-to-use-logging.md)참조).
- JavaScript: 오디오 처리 성능을 향상 시킵니다.

**버그 수정**

- Mac/iOS: 음성 서비스에 대 한 연결을 설정할 수 없는 경우 오랜 대기를 야기 하는 버그를 수정 했습니다.
- Python: Python 콜백에서 인수에 대 한 오류 처리를 향상 시킵니다.
- JavaScript: RequestSession에서 종료 된 음성에 대 한 잘못 된 상태 보고가 수정 되었습니다.

## <a name="speech-sdk-131-2019-february-refresh"></a>Speech SDK 1.3.1:2019-2 월 새로 고침

이 릴리스는 버그 수정 릴리스 이며 네이티브/관리 SDK에만 영향을 줍니다. SDK의 JavaScript 버전에는 영향을 주지 않습니다.

**버그 수정**

- 마이크 입력을 사용할 때 메모리 누수가 수정 되었습니다. 스트림 기반 또는 파일 입력에 영향을 주지 않습니다.

## <a name="speech-sdk-130-2019-february-release"></a>Speech SDK 1.3.0:2019-2 월 릴리스

**새 기능**

- Speech SDK는 클래스를 통해 입력 마이크의 선택을 지원 합니다 `AudioConfig` . 이를 통해 기본이 아닌 마이크에서 음성 서비스로 오디오 데이터를 스트리밍할 수 있습니다. 자세한 내용은 [오디오 입력 장치 선택](how-to-select-audio-input-devices.md)에 대 한 설명서를 참조 하세요. 이 기능은 JavaScript에서 아직 사용할 수 없습니다.
- 이제 Speech SDK는 베타 버전의 Unity를 지원합니다. [GitHub 샘플 리포지토리의](https://aka.ms/csspeech/samples)문제 섹션을 통해 피드백을 제공 합니다. 이 릴리스에서는 Windows x86 및 x64(데스크톱 또는 유니버설 Windows 플랫폼 애플리케이션)와 Android(ARM32/64, x86)의 Unity를 지원합니다. 자세한 내용은 [Unity 빠른 시작](./get-started-speech-to-text.md?pivots=programming-language-csharp&tabs=unity)을 참조하세요.
- `Microsoft.CognitiveServices.Speech.csharp.bindings.dll`이전 릴리스에서 제공 된 파일은 더 이상 필요 하지 않습니다. 이제 기능이 핵심 SDK로 통합 되었습니다.

**샘플**

다음 새 콘텐츠는 [샘플 리포지토리](https://aka.ms/csspeech/samples)에서 사용할 수 있습니다.

- 에 대 한 추가 샘플 `AudioConfig.FromMicrophoneInput` 입니다.
- 의도 인식 및 변환에 대한 추가 Python 샘플
- IOS에서 개체를 사용 하기 위한 추가 샘플 `Connection` 입니다.
- 오디오 출력을 사용한 변환에 대한 추가 Java 예제
- [일괄 처리 기록 REST API](batch-transcription.md)

**향상된 기능/변경 사항**

- Python
  - 에서 매개 변수 확인 및 오류 메시지가 개선 `SpeechConfig` 되었습니다.
  - 개체에 대 한 지원을 추가 `Connection` 합니다.
  - Windows에서 32비트 Python(x86)을 지원합니다.
  - Python용 Speech SDK가 베타를 벗어났습니다.
- iOS
  - SDK는 이제 iOS SDK 버전 12.1용으로 빌드되었습니다.
  - SDK는 이제 iOS 버전 9.2 이상을 지원합니다.
  - 참조 설명서를 개선하고 몇 가지 속성 이름을 수정합니다.
- JavaScript
  - 개체에 대 한 지원을 추가 `Connection` 합니다.
  - 번들로 묶은 JavaScript의 형식 정의 파일을 추가했습니다.
  - 구문 힌트의 초기 지원 및 구현이 제공됩니다.
  - 인식을 위해 서비스 JSON을 사용하는 속성 컬렉션을 반환합니다.
- 이제 Windows DLL이 버전 리소스를 포함합니다.
- 인식기를 만드는 경우 `FromEndpoint` 끝점 URL에 매개 변수를 직접 추가할 수 있습니다. `FromEndpoint`를 사용 하면 표준 구성 속성을 통해 인식기를 구성할 수 없습니다.

**버그 수정**

- 빈 프록시 이름과 프록시 암호가 올바르게 처리되지 않았습니다. 이 릴리스에서는 프록시 이름과 프록시 암호를 빈 문자열로 설정하면 프록시에 연결될 때 제출되지 않습니다.
- SDK에서 만든 SessionId가 항상 일부 언어&nbsp;/ 환경에서 무작위인 것은 아니었습니다. 이 문제를 해결 하기 위해 임의 생성기 초기화를 추가 했습니다.
- 권한 부여 토큰 처리를 개선했습니다. 권한 부여 토큰을 사용 하려면에서를 지정 `SpeechConfig` 하 고 구독 키를 비워 둡니다. 그런 다음, 평소처럼 인식기를 만듭니다.
- 경우에 따라 `Connection` 개체가 올바르게 해제 되지 않았습니다. 이 문제가 해결되었습니다.
- Safari에서도 오디오 출력의 변환 합성을 지원하도록 JavaScript 샘플을 수정했습니다.

## <a name="speech-sdk-121"></a>Speech SDK 1.2.1

JavaScript 전용 릴리스입니다. 추가한 기능은 없습니다. 다음과 같이 수정했습니다.

- speech.end가 아닌 turn.end에서 스트림 끝을 실행합니다.
- 현재 전송이 실패한 경우 다음 전송을 예약하지 않는 오디오 펌프의 버그를 수정했습니다.
- 인증 토큰을 사용한 연속 인식을 수정했습니다.
- 다른 인식기/엔드포인트의 버그를 수정했습니다.
- 설명서 향상된 기능입니다.

## <a name="speech-sdk-120-2018-december-release"></a>Speech SDK 1.2.0:2018-12 월 릴리스

**새 기능**

- Python
  - 이 릴리스에서는 베타 버전의 Python(3.5 이상)이 지원됩니다. 자세한 내용은 여기를 참조 하십시오.] (python.md).
- JavaScript
  - JavaScript용 Speech SDK가 오픈 소스로 제공됩니다. 소스 코드는 [GitHub](https://github.com/Microsoft/cognitive-services-speech-sdk-js)에서 사용할 수 있습니다.
  - 이제 Node.js를 지원합니다. 자세한 정보는 [여기](./get-started-speech-to-text.md)에서 확인할 수 있습니다.
  - 오디오 세션에 대한 길이 제한이 제거되었으므로 백그라운드에서 자동으로 다시 연결됩니다.
- `Connection` 개체의  멤버의 부모에 대해 SQL Server 인스턴스 이름을 표시합니다.
  - 에서 `Recognizer` 개체에 액세스할 수 있습니다 `Connection` . 이 개체를 사용하면 명시적으로 서비스 연결을 시작하고 연결 및 연결 끊기 이벤트를 구독할 수 있습니다.
    이 기능은 JavaScript 및 Python에서 아직 사용할 수 없습니다.
- Ubuntu 18.04 지원
- Android
  - APK 생성 중에 ProGuard 지원이 설정되었습니다.

**개선과**

- 스레드, 잠금, 뮤텍스 수를 줄이면서 내부 스레드 사용이 개선되었습니다.
- 오류 보고/정보가 개선되었습니다. 일부 경우에는 오류 메시지가 모든 방식으로 전파 되지 않습니다.
- 최신 모듈을 사용하도록 JavaScript의 개발 종속성을 업데이트했습니다.

**버그 수정**

- 의 형식 불일치로 인해 메모리 누수가 수정 `RecognizeAsync` 되었습니다.
- 어떤 경우에는 예외가 유출되었습니다.
- 번역 이벤트 인수에서 메모리 누수가 수정되었습니다.
- 장기 실행 세션에서 다시 연결 시 잠금 문제가 해결되었습니다.
- 실패 한 번역의 최종 결과가 누락 될 수 있는 문제를 해결 했습니다.
- C #: 작업이 주 스레드에서 대기 되지 않은 경우에는 `async` 비동기 작업이 완료 되기 전에 인식기를 삭제할 수 있었습니다.
- Java: 문제를 해결 하 여 Java VM의 작동이 중단 되는 문제를 해결 했습니다.
- 목표-C: 열거형 매핑 수정 대신 RecognizedIntent이 반환 되었습니다 `RecognizingIntent` .
- JavaScript:에서 기본 출력 형식을 ' 단순 '으로 설정 `SpeechConfig` 합니다.
- JavaScript: JavaScript 및 기타 언어에서 구성 개체의 속성 간에 불일치를 제거 합니다.

**샘플**

- 여러 샘플 (예: 번역에 대 한 음성 출력 등)을 업데이트 하 고 수정 했습니다.
- Node.js 샘플을 [샘플 리포지토리](https://aka.ms/csspeech/samples)에 추가했습니다.

## <a name="speech-sdk-110"></a>Speech SDK 1.1.0

**새 기능**

- Android x86/x64를 지원합니다.
- 프록시 지원: 개체에서 `SpeechConfig` 이제 함수를 호출 하 여 프록시 정보 (호스트 이름, 포트, 사용자 이름 및 암호)를 설정할 수 있습니다. iOS에서는 아직 이 기능을 사용할 수 없습니다.
- 향상된 오류 코드 및 메시지입니다. 인식이 오류를 반환한 경우 이미 `Reason`(취소된 이벤트의) 또는 `CancellationDetails`(인식 결과의) `Error`로 설정되어 있습니다. 취소 이벤트에는 이제 두 개의 추가 멤버 `ErrorCode` 및 `ErrorDetails`가 포함됩니다. 서버에서 보고된 오류를 사용하여 추가 오류 정보를 반환하는 경우 해당 서버를 새 멤버에서 사용할 수 있습니다.

**개선과**

- 인식기 구성에서 추가 확인을 추가하고, 추가 오류 메시지를 추가했습니다.
- 오디오 파일의 중간에 긴 무음 시간 처리가 향상되었습니다.
- NuGet 패키지: .NET Framework의 경우 프로젝트는 AnyCPU 구성을 통한 빌드를 방지합니다.

**버그 수정**

- 인식기에서 발견된 몇 가지 예외를 수정했습니다. 또한 예외가 catch 되 고 이벤트로 변환 됩니다 `Canceled` .
- 속성 관리에서 메모리 누수를 해결합니다.
- 오디오 입력 파일이 인식기 작동을 중지할 수 있는 버그가 수정되었습니다.
- 세션 중지 이벤트 후 이벤트를 수신할 수 있는 버그가 수정되었습니다.
- 스레딩에서 일부 경합 상태가 수정되었습니다.
- 결국 충돌을 일으킬 수 있는 iOS 호환성 문제가 해결되었습니다.
- Android 마이크 지원의 안정성 향상.
- JavaScript의 인식기가 인식 언어를 무시하는 버그가 수정되었습니다.
- JavaScript에서 (경우에 따라)를 설정 하는 것을 방지 하는 버그를 수정 `EndpointId` 했습니다.
- JavaScript의 AddIntent에서 매개 변수 순서가 변경 되었으며 누락 된 `AddIntent` javascript 서명이 추가 되었습니다.

**샘플**

- [샘플 리포지토리에서](https://aka.ms/csspeech/samples)끌어오기 및 푸시 스트림 사용에 대 한 c + + 및 c # 샘플을 추가 했습니다.

## <a name="speech-sdk-101"></a>Speech SDK 1.0.1

안정성 향상 및 버그 수정:

- 삭제 중인 인식기의 경합으로 인한 잠재적인 심각한 오류가 수정되었습니다.
- 설정 되지 않은 속성이 발생할 때 잠재적 심각한 오류가 수정 되었습니다.
- 추가 오류 및 매개 변수 검사가 추가되었습니다.
- Objective-C: NSString에서 이름 재정의로 인한 잠재적인 심각한 오류가 수정되었습니다.
- Objectice-C: API의 표시 유형이 조정되었습니다.
- JavaScript: 관련 이벤트 및 해당 페이로드가 수정되었습니다.
- 설명서 향상된 기능입니다.

[샘플 리포지토리](https://aka.ms/csspeech/samples)에서 JavaScript에 대한 새로운 샘플이 추가되었습니다.

## <a name="cognitive-services-speech-sdk-100-2018-september-release"></a>Cognitive Services Speech SDK 1.0.0: 2018년 9월 release

**새로운 기능**

- iOS에서 Objective-C를 지원합니다. [iOS용 Objective-C 빠른 시작](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart/objectivec/ios/from-microphone)을 확인하세요.
- 브라우저에서 JavaScript를 지원합니다. [JavaScript 빠른 시작](./get-started-speech-to-text.md)을 확인하세요.

**주요 변경 내용**

- 이 릴리스에서는 몇 가지 주요 변경 사항이 도입 되었습니다.
  자세한 내용은 [이 페이지](https://aka.ms/csspeech/breakingchanges_1_0_0) 를 확인 하세요.

## <a name="cognitive-services-speech-sdk-060-2018-august-release"></a>Cognitive Services Speech SDK 0.6.0: 2018년 8월 릴리스

**새로운 기능**

- Speech SDK를 사용하여 빌드된 UWP 앱은 이제 WACK(Windows 앱 인증 키트)를 전달할 수 있습니다.
  [UWP 빠른 시작](./get-started-speech-to-text.md?pivots=programming-language-chsarp&tabs=uwp)을 확인하세요.
- Linux(Ubuntu 16.04 x64)에서 .NET 표준 2.0을 지원합니다.
- 실험: Windows(64비트) 및 Linux(Ubuntu 16.04 x64)에서 Java 8을 지원합니다.
  [Java Runtime Environment 빠른 시작](./get-started-speech-to-text.md?pivots=programming-language-java&tabs=jre)을 확인하세요.

**기능 변경**

- 연결 오류에 대한 추가 오류 세부 정보를 표시합니다.

**주요 변경 내용**

- Java(Android)에서, `SpeechFactory.configureNativePlatformBindingWithDefaultCertificate` 함수는 더 이상 경로 매개 변수를 요구하지 않습니다. 이제 지원되는 모든 플랫폼에서 경로가 자동으로 검색됩니다.
- Java 및 C#에서 `EndpointUrl` 속성의 get-accessor가 제거되었습니다.

**버그 수정**

- Java에서, 번역 인식기의 오디오 합성 결과가 구현되었습니다.
- 비활성 스레드 및 사용되지 않는 열린 소켓 수가 증가하는 버그가 수정되었습니다.
- 오래 실행되는 인식이 전송 중에 종료될 수 있는 문제가 해결되었습니다.
- 인식기 종료에서 발생하는 경합 조건을 수정했습니다.

## <a name="cognitive-services-speech-sdk-050-2018-july-release"></a>Cognitive Services Speech SDK 0.5.0: 2018년 7월 릴리스

**새로운 기능**

- Android 플랫폼(API 23: Android 6.0 Marshmallow 이상)을 지원합니다. [Android 빠른 시작](./get-started-speech-to-text.md?pivots=programming-language-java&tabs=android)을 확인하세요.
- Windows에서 .NET Standard 2.0을 지원합니다. [.NET Core 빠른 시작](./get-started-speech-to-text.md?pivots=programming-language-csharp&tabs=dotnetcore)을 확인하세요.
- 실험: Windows(버전 1709 이상)에서 UWP를 지원합니다.
  - [UWP 빠른 시작](./get-started-speech-to-text.md?pivots=programming-language-csharp&tabs=uwp)을 확인하세요.
  - 참고: Speech SDK를 사용하여 빌드된 UWP 앱은 아직 WACK(Windows 앱 인증 키트)를 제공하지 않습니다.
- 자동 다시 연결을 통해 장기 실행 인식을 지원합니다.

**기능 변경 내용**

- `StartContinuousRecognitionAsync()`에서 장기 실행 인식을 지원합니다.
- 인식 결과에 더 많은 필드가 포함됩니다. 인식된 텍스트의 오디오 시작 및 지속 시간의 오프셋(두 가지 모두 틱 단위) 및 인식 상태를 나타내는 추가 값(예: `InitialSilenceTimeout`, `InitialBabbleTimeout`)입니다.
- 팩터리 인스턴스를 만들기 위한 AuthorizationToken을 지원합니다.

**주요 변경 내용**

- 인식 이벤트: 이벤트 `NoMatch` 유형이 이벤트에 병합 되었습니다 `Error` .
- C #의 SpeechOutputFormat `OutputFormat` 는 c + +에 맞게 변경 되었습니다.
- `AudioInputStream` 인터페이스의 일부 메서드 반환 형식이 다음과 같이 약간 변경되었습니다.
  - Java에서 `read` 메서드는 이제 `int` 대신 `long`을 반환합니다.
  - C#에서 `Read` 메서드는 이제 `int` 대신 `uint`을 반환합니다.
  - C++에서 `Read` 및 `GetFormat` 메서드는 이제 `int` 대신 `size_t`를 반환합니다.
- C++: 오디오 입력 스트림의 인스턴스가 이제 `shared_ptr`로만 전달될 수 있습니다.

**버그 수정**

- `RecognizeAsync()` 시간이 초과될 때 결과의 잘못된 반환 값이 수정되었습니다.
- Windows에서 미디어 파운데이션 라이브러리에 대한 종속성이 제거되었습니다. SDK에 이제 Core Audio API가 사용됩니다.
- 설명서 수정 사항: 지원되는 지역을 설명하는 [지역](regions.md) 페이지가 추가되었습니다.

**알려진 문제**

- Android용 Speech SDK에서는 번역에 대한 음성 합성 결과를 보고하지 않습니다. 이 문제는 다음 릴리스에서 해결될 예정입니다.

## <a name="cognitive-services-speech-sdk-040-2018-june-release"></a>Cognitive Services Speech SDK 0.4.0: 2018년 6월 릴리스

**기능 변경 내용**

- AudioInputStream

  이제 인식기가 스트림을 오디오 원본으로 사용할 수 있습니다. 자세한 내용은 관련 [방법 가이드](how-to-use-audio-input-streams.md)를 참조하세요.

- 자세한 출력 형식

  `SpeechRecognizer`를 만들 때 `Detailed` 또는 `Simple` 출력 형식을 요청할 수 있습니다. `DetailedSpeechRecognitionResult`에는 신뢰도 점수, 인식된 텍스트, 원시 어휘 형식, 정규화된 형식 및 마스킹된 욕설이 포함된 정규화된 형식이 포함됩니다.

**주요 변경 내용**

- C#의 `SpeechRecognitionResult.RecognizedText`가 `SpeechRecognitionResult.Text`로 변경되었습니다.

**버그 수정**

- 종료하는 동안 USP 계층에서 발생할 수 있는 콜백 문제가 해결되었습니다.
- 인식기가 오디오 입력 파일을 사용한 경우, 필요한 것보다 더 긴 파일 핸들을 사용하고 있었습니다.
- 메시지 펌프와 인식기 간에 여러 가지 교착 상태가 제거되었습니다.
- 서비스 응답 시간이 초과되면 `NoMatch` 결과를 실행합니다.
- Windows의 미디어 파운데이션 라이브러리는 지연 로드됩니다. 이 라이브러리는 마이크 입력에만 필요합니다.
- 오디오 데이터의 업로드 속도는 원본 오디오 속도의 두 배 정도로 제한됩니다.
- Windows에서 C# .NET 어셈블리에 이제 강력한 이름이 지정됩니다.
- 설명서 수정: `Region`은 인식기를 만드는 데 필요한 정보입니다.

추가 샘플이 추가되었고 지속적으로 업데이트되고 있습니다. 최신 샘플 집합은 [Speech SDK 샘플 GitHub 리포지토리](https://aka.ms/csspeech/samples)를 참조하세요.

## <a name="cognitive-services-speech-sdk-0212733-2018-may-release"></a>Cognitive Services Speech SDK 0.2.12733: 2018년 5월 릴리스

이 릴리스는 Cognitive Services Speech SDK의 첫 번째 공개 미리 보기 릴리스입니다.

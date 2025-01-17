---
title: 빠른 시작 - iOS 앱에서 Teams 모임에 조인
description: 이 자습서에서는 iOS용 Azure Communication Services 통화 SDK를 사용하여 Teams 모임에 조인하는 방법을 알아봅니다.
author: chpalm
ms.author: mikben
ms.date: 03/10/2021
ms.topic: quickstart
ms.service: azure-communication-services
ms.openlocfilehash: 8ff85dc5571f549027e208409db3f4e80c68b205
ms.sourcegitcommit: bed20f85722deec33050e0d8881e465f94c79ac2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105108196"
---
이 빠른 시작에서는 iOS용 Azure Communication Services 통화 SDK를 사용하여 Teams 모임에 조인하는 방법을 알아봅니다.

## <a name="prerequisites"></a>필수 조건

- 작동하는 [Communication Services 통화 iOS 앱](../getting-started-with-calling.md).
- [Teams 배포](/deployoffice/teams-install)


## <a name="add-the-teams-ui-controls-and-enable-the-teams-ui-controls"></a>Teams UI 컨트롤을 추가하고 Teams UI 컨트롤을 사용하도록 설정

ContentView.swift의 코드를 다음 코드 조각으로 바꿉니다. 텍스트 상자는 Teams 모임 컨텍스트를 입력하는 데 사용되며, 단추는 지정된 모임에 참가하는 데 사용됩니다.

```swift

import SwiftUI
import AzureCommunicationCalling
import AVFoundation

struct ContentView: View {
    @State var meetingLink: String = ""
    @State var callStatus: String = ""
    @State var message: String = ""
    @State var recordingStatus: String = ""
    @State var callClient: CallClient?
    @State var callAgent: CallAgent?
    @State var call: Call?
    @State var callObserver: CallObserver?

    var body: some View {
        NavigationView {
            Form {
                Section {
                    TextField("Teams meeting link", text: $meetingLink)
                    Button(action: joinTeamsMeeting) {
                        Text("Join Teams Meeting")
                    }.disabled(callAgent == nil)
                    Button(action: leaveMeeting) {
                        Text("Leave Meeting")
                    }.disabled(call == nil)
                    Text(callStatus)
                    Text(message)
                    Text(recordingStatus)
                }
            }
            .navigationBarTitle("Calling Quickstart")
        }.onAppear {
            // Initialize call agent
            var userCredential: CommunicationTokenCredential?
            do {
                userCredential = try CommunicationTokenCredential(token: "<USER ACCESS TOKEN>")
            } catch {
                print("ERROR: It was not possible to create user credential.")
                self.message = "Please enter your token in source code"
                return
            }

            self.callClient = CallClient()

            // Creates the call agent
            self.callClient?.createCallAgent(userCredential: userCredential) { (agent, error) in
                if error == nil {
                    guard let agent = agent else {
                        self.message = "Failed to create CallAgent"
                        return
                    }

                    self.callAgent = agent
                    self.message = "Call agent successfully created."
                } else {
                    self.message = "Failed to create CallAgent with error"
                }
            }
        }
    }

    func joinTeamsMeeting() {
        // Ask permissions
        AVAudioSession.sharedInstance().requestRecordPermission { (granted) in
            if granted {
                let joinCallOptions = JoinCallOptions()
                let teamsMeetingLinkLocator = TeamsMeetingLinkLocator(meetingLink: self.meetingLink);
                guard let call = self.callAgent?.join(with: teamsMeetingLinkLocator, joinCallOptions: joinCallOptions) else {
                    self.message = "Failed to join Teams meeting"
                    return
                }

                self.call = call
                self.callObserver = CallObserver(self)
                self.call!.delegate = self.callObserver
                self.message = "Teams meeting joined successfully"
            }
        }
    }

    func leaveMeeting() {
        if let call = call {
            call.hangup(options: nil, completionHandler: { (error) in
                if error == nil {
                    self.message = "Leaving Teams meeting was successful"
                } else {
                    self.message = "Leaving Teams meeting failed"
                }
            })
        } else {
            self.message = "No active call to hanup"
        }
    }
}

class CallObserver : NSObject, CallDelegate {
    private var owner:ContentView
    init(_ view:ContentView) {
        owner = view
    }

    public func onCallStateChanged(_ call: Call!,
                                   args: PropertyChangedEventArgs!) {
        owner.callStatus = CallObserver.callStateToString(state: call.state)
        if call.state == .disconnected {
            owner.call = nil
            owner.message = "Left Meeting"
        } else if call.state == .inLobby {
            owner.message = "Waiting in lobby !!"
        } else if call.state == .connected {
            owner.message = "Joined Meeting !!"
        }
    }
    
    public func onIsRecordingActiveChanged(_ call: Call!, args: PropertyChangedEventArgs!) {
        if (call.isRecordingActive == true) {
            owner.recordingStatus = "This call is being recorded"
        }
        else {
            owner.recordingStatus = ""
        }
    }

    private static func callStateToString(state: CallState) -> String {
        switch state {
        case .connected: return "Connected"
        case .connecting: return "Connecting"
        case .disconnected: return "Disconnected"
        case .disconnecting: return "Disconnecting"
        case .earlyMedia: return "EarlyMedia"
        case .hold: return "Hold"
        case .incoming: return "Incoming"
        case .none: return "None"
        case .ringing: return "Ringing"
        case .inLobby: return "InLobby"
        default: return "Unknown"
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

```

## <a name="get-the-teams-meeting-link"></a>Teams 미팅 링크 가져오기

Teams 미팅 링크는 Graph API를 사용하여 검색할 수 있습니다. 자세한 내용은 [Graph 설명서](/graph/api/onlinemeeting-createorget?tabs=http&view=graph-rest-beta)에서 설명하고 있습니다.
Communication Services Calling SDK는 전체 Teams 미팅 링크를 수락합니다. 이 링크는 [`joinWebUrl` 속성](/graph/api/resources/onlinemeeting?view=graph-rest-beta)에서 액세스할 수 있는 `onlineMeeting` 리소스의 일부로 반환됩니다. 또한 Teams 모임 초대 자체의 **모임 조인** URL에서 필요한 모임 정보를 가져올 수 있습니다.

## <a name="launch-the-app-and-join-teams-meeting"></a>앱을 시작하고 Teams 모임에 조인

**제품** > **실행** 을 선택하거나 (&#8984;-R) 키보드 단축키를 사용하여 iOS 시뮬레이터에서 앱을 빌드하고 실행할 수 있습니다.

:::image type="content" source="../media/ios/acs-join-teams-meeting-quickstart.png" alt-text="완료된 애플리케이션을 보여 주는 스크린샷":::

Teams 컨텍스트를 텍스트 상자에 삽입하고, *Teams 모임 참가* 를 눌러 Communication Services 애플리케이션 내에서 Teams 모임에 참가합니다.

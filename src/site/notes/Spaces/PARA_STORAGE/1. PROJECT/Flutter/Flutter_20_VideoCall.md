---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-20-video-call/"}
---

# 20. Video Call (영상통화)
- 각 기능은 특정 API 제공자에 의해 종속된 기능이 많았음.

- 이 프로젝트 진행 과정에서 중점으로 공부했던 내용은
	- 프로젝트 구조 작성 방법
	- Permission 관련

- Geolocator에서도 권한 요청이 가능함.

- 권한 요청 2번째 방법
	- Permission.
```dart
Future<void> init() async {  
  final resp = await [Permission.camera, Permission.microphone].request();  
```
- 2가지 권한을 요청할 것임 -> 카메라. 마이크(아마 리스트 내부 순서 유지)

```dart
  
  final cameraPermission = resp[Permission.camera];  
  final microphonePermission = resp[Permission.microphone];  
  
  if (cameraPermission != PermissionStatus.granted ||  
      microphonePermission != PermissionStatus.granted) {  
    throw '카메라 또는 마이크 권한이 없습니다.';  
  }  
```
- PermissionStatus는 타고 들어가면 바로 보임.
	- 내부에 주석 상세하니, 그것을 참고하면 될 듯.

```dart
  
  if (engine == null) {  
    engine = createAgoraRtcEngine();  
  
    await engine!.initialize(  
      RtcEngineContext(  
        appId: appId,  
      ),  
    );  
  
    engine!.registerEventHandler(  
      RtcEngineEventHandler(  
        onJoinChannelSuccess: (  
          RtcConnection connection,  
          int elapsed,  
        ) {},  
        onLeaveChannel: (  
          RtcConnection connection,  
          RtcStats stats,  
        ) {},  
        onUserJoined: (  
          RtcConnection connection,  
          int remoteUid,  
          int elapsed,  
        ) {  
          print('---User Joined---');  
          setState(() {  
            this.remoteUid = remoteUid;  
          });  
        },  
        onUserOffline: (  
          RtcConnection connection,  
          int remoteUid,  
          UserOfflineReasonType reason,  
        ) {  
          setState(() {  
            this.remoteUid = null;  
          });  
        },  
      ),  
    );  
  
    await engine!.enableVideo();  
    await engine!.startPreview();  
  
    ChannelMediaOptions options = ChannelMediaOptions();  
  
    await engine!.joinChannel(  
      token: token,  
      channelId: channelName,  
      uid: uid,  
      options: options,  
    );  
  }  
}
```
-> 이것들은 특정 api 제공자에 종속된 코드임. 구조가 핵심!
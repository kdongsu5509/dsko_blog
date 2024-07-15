---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-17-video-player/"}
---

# 17. Video_Player
## textStyle.copywith()
```dart
class _Title extends StatelessWidget {  
  const _Title({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    final TextStyle textStyle = TextStyle(  
        color: Colors.white,  
        fontSize: 24);  
    return Row(  
      mainAxisAlignment: MainAxisAlignment.center,  
      children: [  
        Text(  
          'Video',  
          style: textStyle.copyWith(  
            fontWeight: FontWeight.w200,  
          ),  
        ),  
        Text(  
          'Player',  
          style: textStyle.copyWith(  
            fontWeight: FontWeight.bold,  
          ),  
        ),  
      ],  
    );  
  }  
}
```
- 해당 함수 -> 덮어쓰기
	- 기존 textstyle에 부족한 부분은 추가되어서, 기존 존재하던 부분은 덮어씀.

## Gradation
```dart
Widget build(BuildContext context) {  
  return Scaffold(  
    body: Container(  
      width: double.infinity,  
      decoration: BoxDecoration(  
        gradient: LinearGradient(  
          begin: Alignment.topCenter, // 시작점  
          end: Alignment.bottomCenter, // 끝점  
          // stops:  
          // [          //   0.1,          //   0.9,          // ], 그라데이션 범위 지정  
          colors: [  
            Color(0xFF2A3A7C),  
            Color(0xFF000118),  
          ],  
        ),  
  
      ),  
      child: Column(  
        mainAxisAlignment: MainAxisAlignment.center,  
        children: [  
          _Logo(),  
          const SizedBox(height: 28),  
          _Title(),  
        ],  
      ),  
    ),
```
- decoration 파라미터에 BoxDecoration() 위젯 넣기
	- color 지정 수에 맞게 begin, end 넣어야 에러 안발생 -> 아니면 색깔 적용 안됨.
	- gradient 파라미터 : 그라데이션이 어떤 모양으로 적용될지 선택.

## Ternary Operator로 위젯 스위칭하기
##### 터치 인식 기능 추가
```Dart
Widget build(BuildContext context) {  
  return GestureDetector(  
    onTap: () {},  
    child: Image.asset('asset/image/logo.png'),  
  );  
}
```
- 원래 Image는 터치 x
- GestureDetector로 감싸는 순간 가능!
	- child 반응 탐지
	- onTap : 터치를 입력받음.

## 동영상 선택하는 기능 구현하기
`video_player:
{ #2}
.8.2` : 영상 관련 기능을 제공하는 외부 플러그인
`image_picker:
{ #1}
.0.7` : 이미지 선택에 관련된 기능을 제공하는 외부 플러그인

```dart
onLogoTap() async {  
  final video = await ImagePicker().pickVideo(  
    source: ImageSource.gallery,  
  );  
  
  setState(() {  
    this.video = video;  
  });  
}
```

`No implementation found` : 에러의 한 종류 : 
- terminal에서 flutter clean 입력 후 다시 시작하면 해결 가능(ios)
	- native 관련 코드가 필요한 경우에, 동기화가 안되어 있으면 발생

Android의 경우
터미널에서 flutter run 실행(프로젝트 파일 위치여야 함.)
이후 `please choos one`에서 디바이스 선택 후 multidex support ~~ 가 발생 -> 이떄 y 눌러서 동기화 가능


-> 나머지는 수기로 정리! -> 좀 검토할 것이 많음.
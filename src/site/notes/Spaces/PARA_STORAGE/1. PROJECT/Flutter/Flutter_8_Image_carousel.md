---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-8-image-carousel/"}
---

# 13. Image Carousel (전자액자)
## Timer
- 지정한 시간이 지난 뒤 한 번 또는 주기적으로 무언가를 실행 할 수 있게 해주는 위젯
- dart:async(기본 제공) ; pubspec.yaml에서 설정 x

###### Single
```DART
import 'dart/async'

void maiN(){
	Timer(
		Duration(seconds : 1),
		() {
			print('1초 뒤 실행');
		}
	)
}
```
- 첫 번째 파라미터 : Duration
- 두 번째 파라미터 : 실행 함수.

+)추가 : Dart의 익명, 람다 함수
```dart
// 일반 익명 함수
var printMessage = (String message) {
  print(message);
};

// 람다 함수
var add = (int a, int b) => a + b;
```

###### Multi
```Dart
import 'dart/async'

void maiN(){
	Timer.periodic( //반복 실행 위해 .periodic 생성자 사용
		Duration(seconds : 1),
		(Timer timer) {
			print('1초 뒤 실행');
		}
	)
}
```
- 첫 번째 파라미터 : Duration
- 두 번째 파라미터 : 실행 함수.
	- 파라미터에 Timer timer 추가 -> 타이머의 인스턴스 반환
	- 반복 종료 조건을 위해.(timer.cancel)

Timer.canel() 예시
```dart
import 'dart:async';

void main() {
  
  int num = 0;
  
  Timer.periodic(
    Duration(seconds: 1),
    (Timer timer) {
      num++;
      print('1초 뒤에 실행한다!');
      
      if(num == 12){
        timer.cancel();
      }
    },
  );
}

```

## PageView을 이용한 코드
```Dart
import 'package:flutter/material.dart';  
  
class HomeScreen extends StatelessWidget {  
  const HomeScreen({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    return Scaffold(  
      body: PageView(  
        children: [1, 2, 3, 4, 5]  
            .map((e) => Image.asset(  
                  'asset/img/image_$e.jpeg',  
                  fit: BoxFit.cover,  
                ))  
            .toList(),  
      ),  
    );  
  }  
}
```
- PageView => [[Spaces/PARA_STORAGE/1. PROJECT/Flutter/Flutter_pageView\|Flutter_pageView]]

```dart
import 'package:flutter/material.dart';  
import 'dart:async';  
  
class HomeScreen extends StatefulWidget {  
  const HomeScreen({super.key});  
  
  @override  
  State<HomeScreen> createState() => _HomeScreenState();  
}  
  
class _HomeScreenState extends State<HomeScreen> {  
  Timer? timer;  
  
  PageController controller = PageController();  
  
  @override  
  void initState() {  
    // TODO: implement initState  
    super.initState();  
  
    timer = Timer.periodic(  
      Duration(seconds: 2),  
        (timer) {  
        int currentPage = controller.page!.toInt();  
        int nextPage = currentPage + 1;  
        if (nextPage > 4) {  
          nextPage = 0;  
        }  
  
        controller.animateToPage(  
          nextPage,  
          duration: Duration(milliseconds: 300),  
          curve: Curves.linear,  
        );  
      },  
    );  
  }  
  
  @override  
  void dispose() {  
    if (timer != null){  
      timer!.cancel();  
    }  
    controller.dispose();  
    super.dispose();  
  }  
  
  @override  
  Widget build(BuildContext context) {  
    return Scaffold(  
      body: PageView(  
        controller: controller,  
        children: [1, 2, 3, 4, 5]  
            .map((e) =>  
            Image.asset(  
              'asset/img/image_$e.jpeg',  
              fit: BoxFit.cover,  
            ))  
            .toList(),  
      ),  
    );  
  }  
}
```
-curve : [curve 관련 effect 보기](https://api.flutter.dev/flutter/animation/Curves-class.html)

[[Spaces/PARA_STORAGE/1. PROJECT/Flutter/Flutter_Controller\|Flutter_Controller]]
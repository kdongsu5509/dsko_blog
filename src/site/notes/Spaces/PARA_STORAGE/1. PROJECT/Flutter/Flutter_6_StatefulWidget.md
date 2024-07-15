---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-6-stateful-widget/"}
---

```toc
```
# 11. StatefulWidget
## StatefulWidet
**EveryThing is Widget**
- 플러터는 화면에 보여지는 요소를 클래스로 표현, 이를 위젯이라 명명
- 모든 위젯은 Immutable.
	- 그렇다면, 화면 내 변경은?? -> 덮어쓰기(by build())

**UI widget
- StatelessWidget
	-  `HotReload` 로 변경가능.
		- 그러나, 해당 기능은 개발 단계의 개발자만 볼 수 있음
- StatefulWidget
	-  `setstate(함수)` 함수를 이용해 상태 변경 가능.
- 형태 : 클래스 2개 필요. 둘이 연동되어 있음.
```Dart
class HomeScreen extends StatefulWidget{
	@Override
	State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
	~~~
}
```

+) 플러터 프레임워크는 최초로 앱을 실행시킬 때 2번 빌드를 실행함.
## 실습코드
```Dart
import 'package:flutter/material.dart';  
  
class HomeScreen2 extends StatefulWidget {  
  State<HomeScreen2> createState() => _HomeScreen2State();
  ///화살표 연산자(=>)
  ///반환 타입 : Sate<HomeScreen2>
	  ///State클래스 : StatefulWidget과 연결되어 위젯의 상태를 관리하고, 화면의 상태 변화에 따른 뷰의 업데이트를 담당 / build() 메서드를 포함하며, 이 메서드에서는 실제 위젯의 렌더링을 정의
}  
  
class _HomeScreen2State extends State<HomeScreen2>{  
  Color color = Colors.blue;  
  
  @override  
  Widget build(BuildContext context) {  
    return Scaffold(  
      body: Container(  
        width: double.infinity,  
        child: Column(  
          mainAxisAlignment: MainAxisAlignment.center,  
          children: [  
            ElevatedButton(  
              onPressed: () {  
                if(color == Colors.blue){  
                  color = Colors.red;  
                }else{  
                  color = Colors.blue;  
                }  
  
                print('color : $color');  
  
                setState(() {  
                  color = color;  
                });  
              },  
              child: Text('색상 변경!'),  
            ),  
            const SizedBox(height: 32),  
            Container(  
              width: 50.0,  
              height: 50.0,  
              color: color,  
            )  
          ],  
        ),  
      ),  
    );  
  }  
}
```

---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-7-widget-life-cycle/"}
---

```toc
```
# 12. Widget Life Cycle
## StatelessWidget 라이프 사이클
- Step1 : Constructor() 호출 -> Step2 : Build() 호출 : 화면 생성.
### 실습코드
```dart
import 'package:flutter/material.dart';  
  
class HomeScreen extends StatelessWidget {  
  const HomeScreen({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    return Scaffold(  
      body: CodeFactoryWidget(),  
    );  
  }  
}  
  
class CodeFactoryWidget extends StatelessWidget {  
  CodeFactoryWidget({super.key}){  
    print('CodeFactoryWidget constructor');  
  }  
  
  @override  
  Widget build(BuildContext context) {  
    print('CodeFactoryWidget build');  
    return Container(  
      width: 50.0,  
      height: 50.0,  
      color: Colors.red,  
    );  
  }  
}
```

+) 위의 `CodeFactoryWidget` 의 생성자를 Const Constructor로 생성할 수 없는 이유.

- Const와 final의 차이.
	- const : 
	- final : 
- 그렇다면.... 코드는 const 대상일까? -> 답은 X
	- 코드는 JIT 컴파일.
		- 기본:  JIT(Just-In-Time) 컴파일러를 사용하여 코드를 실행 ; 코드를 필요에 따라 바로 컴파일하여 기계어로 변환
		- 하지만 `const`는 이 JIT 컴파일과는 다르게, 코드를 미리 컴파일할 때 이미 결정된 상수 값을 사용하여 최적화하는 것입니다.따라서 Dart에서 `const`는 컴파일 시간에 결정되고 최적화되는 상수 값들을 지정하는 데 사용됨.
## StatefulWidget 라이프 사이클
- **Type1**
![statefulWidgeLifeCycle.png](/img/user/Spaces/included%20image/statefulWidgeLifeCycle.png)
- CodeFactoryWidget -> `StatefulWidget`
-  `StatefulWidget` 위젯이 화면에 표시될 때 내부적으로 상태 클래스 (`State<T>`)가 생성되어 상태를 관리
	- 여기서 `T`는 해당 `StatefulWidget`의 타입
	- 상태 클래스는 위젯의 상태를 관리하고 상태가 변경될 때마다 화면을 다시 렌더링
###### StatefulWidget과 State 클래스의 관계
- StatefulWidget 역시 Widget -> 즉 immutable.
	- 그래서 상태를 관리할 수 있는 상태 객체(`state<T>`) 를 생성.
	- by createState().
- State(`T`)
	- `StatefulWidget`과 연결된 상태를 관리
	-  `setState` 메서드를 호출하여 UI를 갱신
	- `StatefulWidget`의 생명주기 동안 여러 번 생성되고 파괴될 수 있음.
	- -> 그것이 위의 라이프 사이클
		- 1. StatefulWidget이 생성
			- Contstructor()
			- createState()
		- 2. createState()를 통해 생성되는 `State<T>` 상태 객체.
			- initState() -> 일단 초기화
			- didChangeDependencies() --?
			- 현재 상태 : dirty (아직 build 안됨)
			- build() -> 
				- 여기서 setState()를 통해 다시 dirty로 변경할 수도 있다 -> Type2
			- 지금 상태 : clean(build 완료)
		- 3. 다 사용했으면 삭제.
			- deactivate()
			- dispose()



**Type2**
![stateset 라이프 사이클.png](/img/user/stateset%20%EB%9D%BC%EC%9D%B4%ED%94%84%20%EC%82%AC%EC%9D%B4%ED%81%B4.png)
- setState() 내 코드 실행은 dirty상태로 변경 전에 수행.

**Type3**
![lifecycle3_code.png](/img/user/Spaces/included%20image/lifecycle3_code.png)
- 구조
HomeScreen (StatefulWidget)
└── _HomeScreenState (State)
    └── GestureDetector
        └── onTap: () {
              setState(() {
                color = color == Colors.red ? Colors.blue : Colors.red;
              });
            }
        └── child: CodeFactoryWidget (StatefulWidget)
            └── _CodeFactoryWidgetState (State)
                └── Container
                    └── width: 50.0
                    └── height: 50.0
                    └── color: widget.color (Colors.red or Colors.blue)

- **상황**
	- HomeScreen.HomeScreenState.GestureDetector 내에서 setState()가 수행됨.
		- 따라서 build()가 재실행.
		- 이 때 build() 안에 CodeFactoryWidget이 존재!!
	- CodeFacotryWidget과 그의 상태 위젯은 이미 당연히 최초 build시에 build 완료됨.

**Logic
![lifecycle3.png](/img/user/lifecycle3.png)
- 일단 build()가 상위 class에 의해서 실행되면,
	- 다시 Constructor 실행
	- 이 때, 이미 기존 상태 위젯 존재하므로 createState() 미 이행.
		- 이미 존재하던 상태 위젯이므로 initState()랑 didChageDependencies()도 미이행.
	- didUpdateWidget() 실행 
	- 그런데, build() 기록은 새로 만들어진 내 기준에선 없으니 상태가 dirty.
		- 그래서 build() 후 상태 clean으로 변경.
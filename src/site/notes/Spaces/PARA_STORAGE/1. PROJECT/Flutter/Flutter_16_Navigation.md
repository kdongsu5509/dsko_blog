---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-16-navigation/"}
---

# 16. Navigation
## Layout.
- Layout를 설정하여 디자인의 일관성을 유지할 수 있음.
- Appbar 사용 시, 만약 Route Stack 안에 이전 페이지가 있을 시 `자동으로` 뒤로 가기 버튼이 생김.

## Argument 보내기
**알고 있는 방법**
- 매개 변수로 보내기.

```Dart
/// home_screen
ElevatedButton(  
  onPressed: () async {  
    final result = await  
    Navigator.of(context).push(  
      MaterialPageRoute(  
          builder: (BuildContext context) {  
            return RouteOneScreen(number: 20);  
          },  
      ),  
    );  
    print(result);  
  },
```

```dart
///route_One_screen
class RouteOneScreen extends StatelessWidget {  
  final int? number;  
  
  const RouteOneScreen({required this.number, super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    return DefaultLayout(  
      title: 'Route One',  
      children: [  
        Text(  
          'Number: $number',  
          textAlign: TextAlign.center,  
        ),  
        ElevatedButton(  
          onPressed: () {  
            Navigator.of(context).pop(  
              456  
            );  
          },  
          child: Text('Back'),  
        ),  
      ],  
    );  
  }  
}
```


**2번째 방법**

- 전송자
```dart
OutlinedButton(  
  onPressed: () {  
    Navigator.of(context).push(  
      MaterialPageRoute(  
        builder: (BuildContext context) {  
          return RouteTwoScreen();  
        },  
        settings: RouteSettings(  
          arguments: 777,  
        ),  
      ),  
    );  
  },  
  child: Text('Push'),  
)
```
- MaterialPageRoute의 builder와 나란히 settings에서 전달.
	- RouteSettings() 로 감싸서.

- 받는 쪽
```dart
class RouteTwoScreen extends StatelessWidget {  
  const RouteTwoScreen({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    final arguments = ModalRoute.of(context)?.settings.arguments;  
  
    return DefaultLayout(  
      children: [  
        Text(  
          'Arguments: $arguments',  
          textAlign: TextAlign.center,  
        ),  
        OutlinedButton(onPressed: (){  
          Navigator.of(context).pop();  
        }, child: Text('Pop'),)  
      ],  
      title: 'Route Two',  
    );  
  }  
}
```

- 핵심
	- final arguments = ModalRoute.of(context)?.settings.arguments;  

---
---
---

## Declarative Routing과 Named Routes

플러터에서 라우팅은 애플리케이션 내에서 화면 간 전환을 처리하는 방법을 의미합니다. Flutter는 다양한 라우팅 방법을 제공하며, 이 중 대표적인 두 가지는 **Declarative Routing**과 **Named Routes**입니다.

### 1. Declarative Routing

Flutter의 기본적인 설계 철학은 선언적(declarative) 스타일로 구성됩니다. Declarative Routing은 이 철학을 따르는 라우팅 방법으로, UI 상태에 따라 화면을 조건부로 렌더링하는 방식입니다. 이는 `Navigator` 위젯과 함께 사용되며, 특히 `Navigator.push` 및 `Navigator.pop` 메서드를 사용하여 라우트를 관리합니다.

#### 예시

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
          child: Text('Go to Second Screen'),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Second Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: Text('Go back'),
        ),
      ),
    );
  }
}
```

이 예시는 `Navigator.push`와 `Navigator.pop`을 사용하여 두 화면 간의 전환을 관리합니다.

### 2. Named Routes

Named Routes는 라우트를 문자열 이름으로 정의하고 관리하는 방법입니다. 이는 특히 애플리케이션이 커지고, 여러 개의 화면이 있을 때 라우트를 쉽게 관리할 수 있는 방법을 제공합니다. `MaterialApp`의 `routes` 속성을 사용하여 라우트를 설정할 수 있습니다.

#### 예시

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      /// key = 라우트 이름
      /// value - builder -> 이동하고 싶은 라우트
      routes: {
        '/': (context) => HomeScreen(),
        '/second': (context) => SecondScreen(),
      },
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.of(context).pushNamed('/second', arguments : 1111);
          },
          child: Text('Go to Second Screen'),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
	final arguments = ModalRoute.of(context).settings.arguments;
	/// arguments로 받았지만 사용하는 코드는 제외.
    return Scaffold(
      appBar: AppBar(title: Text('Second Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: Text('Go back'),
        ),
      ),
    );
  }
}
```

이 예시는 라우트를 문자열로 정의하고 `Navigator.pushNamed`를 사용하여 화면 전환을 수행합니다.

### 요약

- **Declarative Routing**: `Navigator.push`와 `Navigator.pop`을 사용하여 화면 간 전환을 처리합니다. 코드가 직관적이고 상태에 따라 UI를 동적으로 조정할 수 있습니다.
- **Named Routes**: `MaterialApp`의 `routes` 속성을 사용하여 라우트를 정의하고, 문자열 이름을 통해 라우트를 관리합니다. 특히 애플리케이션이 커질 때 라우트 관리가 용이합니다.
	- MaterialApp에서 라우트 이름 관리해서 한 눈에 파악 가능.
	- 코드의 길이가 줄어듦. -> 유지보수 개꿀

이 두 가지 방법은 각각의 장단점이 있으므로, 애플리케이션의 구조와 요구사항에 따라 적절한 방법을 선택하여 사용할 수 있습니다.


---
---
## pushReplacement
```dart
OutlinedButton(  
  onPressed: () {  
      MaterialPageRoute(  
        builder: (BuildContext context) {  
          return RouteThreeScreen();  
        },  
        settings: RouteSettings(  
          arguments: 999,  
        ),  
      ),  
    );  
  },  
  child: Text('Push Replacement'),  
),  
OutlinedButton(  
  onPressed: () {  
    Navigator.of(context).pushReplacementNamed(  
      '/three',  
      arguments: 999,  
    );  
  },  
  child: Text('Push Replacement Named'),  
),
```
- Route Stack에서의 차이 발생
	- 일반적인 Push
		- [HomeScreen, RouteOneScreen, RouteTwoScreen, RouteThreeScreen] 
	- pushReplacement
		- [HomeScreen, RouteOneScreen, RouteThreeScreen]    
	- 구조
		- Navigator.of(context).pushReplacement(  )

## pushAndRemoveUntil()
```dart
OutlinedButton(  
  onPressed: () {  
    Navigator.of(context).pushNamedAndRemoveUntil(  
      '/three',  
      (route){  
        /// 만약에 삭제 할거면 (Route Stack) false 반환  
        /// 만약에 삭제를 안할거면 true 반환  
        return route.settings.name == '/';  
      },  
      arguments: 999,  
    );  
  },  
  child: Text('Push Named And Remove Until'),  
),
```
- stack에서 원하는거 다 삭제 가능!!

## maybePop()
```dart
OutlinedButton(  
  onPressed: () {  
    Navigator.of(context).maybePop(  
      456,  
    );  
  },  
  child: Text('Maybe Pop'),  
),
```
- 만약 pop이 발생할 경우 stack 이 empty가 되는 경우를 제외하고 정상적으로 pop

## canPop()
```dart
OutlinedButton(  
  onPressed: () {  
    print(Navigator.of(context).canPop());  
  },  
  child: Text('Can Pop'),  
)
```
- canPop()은 결과값 반환함.
	- 스택이 비는 것을 방지함.
## popScope위젯
```dart
PopScope(  /// <<<--- 여기 PopScope!!!
  canPop: false,  
  child: DefaultLayout(  
    title: 'HomeScreen',  
    children: [  
      OutlinedButton(  
        onPressed: () async {  
          final result = await Navigator.of(context).push(  
            MaterialPageRoute(  
              builder: (BuildContext context) {  
                return RouteOneScreen(  
                  number: 20,  
                );  
              },  
            ),
            /// 이하 생략
```
- 시스템의 뒤로가기 기능 모두 block
	- route stack 이 모두 꺼지는 것을 방지.
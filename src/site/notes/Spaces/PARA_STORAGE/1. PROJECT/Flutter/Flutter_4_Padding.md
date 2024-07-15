---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-4-padding/"}
---

# 4. Padding

## Form
```dart
class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Container(
          color: Colors.red,
          child: Padding(
            padding: EdgeInsets.fromLTRB(
              32.0,
              64.0,
              16.0,
              8.0,
            ),
            child: Container(
              color: Colors.blue,
              width: 50.0,
              height: 50.0,
            ),
          ),
        ),
      ),
    );
  }
}
```
- Padding 적용 대상을 Padding 위젯으로 감싼다.
	- Padding 위젯의 padding 파라미터 값으로 옵션 적용.
		- paddding = EdgeInsets.all(double k) : k pixel 만큼 패딩 적용
		- padding = EdgeInsets.symmetric(horizontal : n, vertical : m,)
			- 좌우, 혹은 상하로 같은 패딩 적용
			- 파라미터 둘 중 하나는 반드시 있어야 함.
				- horizontal = 좌우
				- verticla = 상하
		- padding = EdgeInsets.only( top: , left: , right: , buttom: ,)
			- 4개 다 각각 설정 가능- > 안넣으면 0.
		- padding = EdgeInsets.fromLTRB(a,b,c,d)
			- 순서대로 입력
			- 4개 다 넣어야함.
- Padding은 내 주변 울타리 공간임 -> 색깔 x -> 부모 색이 보임.

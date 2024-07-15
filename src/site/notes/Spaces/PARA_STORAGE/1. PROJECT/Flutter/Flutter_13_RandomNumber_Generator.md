---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-13-random-number-generator/"}
---

# 13. Random Number Generator
## Button 스타일 기본
```Dart
ElevatedButton(
	onPressed: () {}
	style: ElevatedButton.styleFrom(
		backgroundColor: ~~
		foregroundColor: ~~
	)
	~~~~
)
```
- 버튼은 효과가 추가로 들어가기 때문에 일반적인 style 지정으로 설정 x
	- backgourndColor : 일반적인 설정과 동일
	- foregroundColor: 클릭 시 나타나는 색깔 -> backgorundColor를 덮음.

## 페이지 전환
- route stack을 이용해서 페이지 전환을 관리

- 페이지 전환 구현 step1. 전환할 페이지 작성
	- 전환할 페이지는 아예 새로운 페이지임. 그러므로 Scaffold 안에서 다시 구조 잡아함.
- 페이지 전환 구현 step2. Navigator을 이용.(PUSH)
```dart
onSettingIconPressed() {
	Navigator.of(context).push(
		MaterialPageRoute(
			builder: (BuildContext context) {
				return 불러올_페이지(전달값);
			},
		),
	);
}
```
 - Navigator 위젯의 도움으로 구현.
	 - context : 위젯 트리 관련 정보 가지고 있음
	 - stateless에서는 기존 context에 전역으로 접근 불가. 그러나 stateful에서는 가능.
 - MaterialPageRoute : 페이지 간 전환 시 효과 및 데이터 전달을 위해 사용.

- 페이지 전환 구현 step3. POP()
```Dart
Navigator.of(context).pop(반환값);
```
- route stack에서 빼내면 끝임.
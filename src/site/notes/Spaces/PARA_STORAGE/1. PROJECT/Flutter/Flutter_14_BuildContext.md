---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-14-build-context/"}
---

# 14. BuildContext
BuildContext는 위젯 트리에서의 위젯의 위치 정보를 들고 있다.

- 하나의 위젯은 자신이 위젯트리의 어디에 위치하고 있는지 어떻게 알까?
	- 위젯 자체는 이 정보를 들고 있지 않는다.

- Widget 내부에 createElement() 라는 함수가 존재
	- Element 제작
		- widget -> 위젯의 종류
		- parent
		- children
		- size
		- Render Objet

- Element는 BuildContext다.
	- BuildContext => 인터페이스
	- Element : BuildContext를 implements로 받은 Class 

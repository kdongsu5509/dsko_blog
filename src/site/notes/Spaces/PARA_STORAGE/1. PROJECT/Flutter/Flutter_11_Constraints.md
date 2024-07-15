---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-11-constraints/"}
---

# 16. Constraint
**Single Pass** ; [[Spaces/PARA_STORAGE/1. PROJECT/Flutter/Flutter_SinglePass\|Flutter_SinglePass]]
**Constraints Go Down**
- 크기의 제약을 의미 ; 제약은 아래로 전가된다.
- 자식 위젯의 크기는 부모 위젯의 크기보다 커질 수 없음.
- 4개의 값으로 setting
	- Max Height
	- Min Height
	- Max Width
	- Min Width
**Sizes Go UP**
- 자식 위젯에서 부모 위젯으로 본인의 사이즈를 전달
**Parent Sets Positon
- 부모 위젯에서 자식 위젯의 크기를 받은 다음에 위치를 지정

**제한 사항들**
- 자식 위젯은 부모 위젯이 제한하고 있는 constraint 내부에서만 크를 가져갈 수 있다.
- 위젯의 위치는 부모 위젯이 지정하기 때문에 위젯은 자신이 정확히 어디에 위치될지 알 수 없다
	- (코드 상에서 x,y 좌표로 위젯을 배하지 않는 이유)
**자식 위젯이 어디에 정렬되어야 하는 지 정확히 알 수 없는 경우는 자식 위젯의 크기가 무시 될 수 있다.**
- 플러터 위젯 중에서는 기본 위치가 지정되어 있는 것이 있고, 아닌 것이 있음.
		- Container : 기본 위치가 지정되어 있지 않음. -> 사이즈가 무됨. 그래서 부모 사이즈 만큼 되버림 ㅠㅠ
		- Row, Column : 기본 위치가 지정되어 있음. : 기본 위치대로 사이즈가 인정되면서 할당됨.
	- 굳이 기본 위치가 지정되어 있는 위젯을 기억할 필요성은 없음.
	- 그냥 위의 제한 사항들 중 마지막 제한 사항을 꼭 기억하면 됨.

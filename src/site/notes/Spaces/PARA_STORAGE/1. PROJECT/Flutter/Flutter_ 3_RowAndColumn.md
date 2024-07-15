---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-3-row-and-column/"}
---

# 3. Row & Column

## Basic
- Row 위젯
	- 가로로 위젯을 배치할 때 사용
	- `children: []` 으로 여러 자식 배치 가능
- Column 위젯
	- 세로로 위젯을 배치할 때 사용
	- `children: []` 으로 여러 자식 배치 가능
- MainAxisAlignment : Row, Column 둘 다에 존재하는 파라미터, 주축을 의미
	- MainAxisSize 라는 파라미터를 통해 크기 지정도 가능.
	- **MainAxisAligment's Options.**
		- MainAxisAlignment.start : 주축의 시작에 정렬
			- row의 경우 왼쪽부터 정렬
			- column의 경우 위로 정렬
		- MainAxisAlignment.end: 주축의 끝에 정렬
			- row의 경우 오른쪽부터 정렬
			- column의 경우 아래로 정렬
		- MainAxisAlignment.center: 주축의 중앙에 정렬
		- MainAxisAlignment.spaceBetween: 주축에서 위젯들 사이에 동일한 간격을 두고 정렬
			- 양 끝 위젯은 양 끝에 위치.
		- MainAxisAlignment.spcaeAround: 주축에서 위젯들 주변에 동일한 간격을 두고 정렬
			- 주변..?
				- *let `\n` is a space and  A, B, C are widgets, A != B != C*
				- Row
					- `\nA\n\nB\n\nC\n` : 주변에 1씩, 그래서 위젯들 사이에는 2씩.
				- Colum은 Row을 90도 회전한 것과 동일.
		- MainAxisAlignment.spaceEvenly: 주축에서 위젯들 앞뒤 및 사이에 동일한 간격을 두고 정렬.
			- ??
				- *let `\n` is a space and  A, B, C are widgets, A != B != C*
				- Row
					- `\nA\nB\nC\n` : 모든 공백 사이즈가 동일.
				- Colum은 Row을 90도 회전한 것과 동일


- CrossAxisAlignment : Row, Column 둘 다에 존재하는 파라미터, 반대축을 의미
	- **CrossAxisAlignment's Options**
		- CrossAxisAlignment.start : 반대축의 시작에 정렬
		- CrossAxisAlignment.end: 반대축의 끝에 정렬
		- CrossAxisAlignment.center: 반대축의 중앙에 정렬
		- CrossAxisAlignment.stretch: 반대축으로 위젯들을 최대로 확장
			- 주축이 Row인 경우에 세로로 확장
			- Column인 경우에는 가로로 확장
		- CrossAxisAlignment.baseline: 텍스트 기준선을 기준으로 위젯을 정렬
			- Option1. TextBaseline.alphabetic : y을 쓸 때 y의 꼬리가 정렬선 벗어나는 것.
			- Option2. TextBaseline.ideographic : 줄노트 쓸 때 g,y, 같은 알파벳을 꼬리까지 포함하여 한 칸에 적는 방식 

- *특별한 제한 사항이 없다면 Row 위젯과 Column 위젯의 주축은 최대 크기를 차지*
- *반대축은 최소 크기를 차지.*
	- 최소 크기: 만약 자식 위젯이 존재한다면 자식 위젯의 사이즈!
		- 자식보다 작아질 수는 없음.

## Expanded & Flexible Widget 
- **Flexible 위젯 Definition** 
```dart
class Flexible extends ParentDataWidget<FlexParentData> {  
  /// Creates a widget that controls how a child of a [Row], [Column], or [Flex]  
  /// flexes.  const Flexible({  
    super.key,  
    this.flex = 1,  
    this.fit = FlexFit.loose,  
    required super.child,  
  });
```
- Paramet explanation
	- key = flexible 위젯 간 차지할 공간에 대한 비율 설정 가능.
	-  fit : if fit.tight -> 가능한 최대 공간 차지

 *expanded는 flexible 위젯을 상속받아서 더 제한을 설정해놓은 것임.*

**Expanded Widget**
- 다 내꺼야 마인드 위젯 -> 모든 공간 다 차지.
	- 다른 위젯 (예 : Container )와 동시 사용 시
		- Contatiner 위젯에 공간 일부만 할당해주고 Expanded가 다 차지
		- Container에게 Container가 필요하다고 한 공간 쥐꼬리만큼 할당해주고, 나머지는 Expand가 다 먹음
	- Expand 2개 이상이면 n 빵.
		- Expanded 내 flex가 기본으로 1로 할당됨. (Default.)
	- 만약 flex를 명시적으로 지정 시
		- 만약 3개 위젯이 다 expanded이고, flex 값이 2,1,1이면 화면에서도 2 : 1 : 1 .

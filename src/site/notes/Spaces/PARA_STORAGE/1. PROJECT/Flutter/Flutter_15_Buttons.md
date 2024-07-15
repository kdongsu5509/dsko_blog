---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-15-buttons/"}
---

# 15. Buttons.
## 기본 버튼 타입 3개
- ElevatedButton
- OutlinedButton
- TextButton

## OutlineButton과 TextButton
```Dart
ElevatedButton(
              /// onPressed: null, // 비활성화
              onPressed: (){},
              style: ElevatedButton.styleFrom(
                backgroundColor: Colors.red,
                disabledBackgroundColor: Colors.grey, // 비활성화 시 배경색
                /// 배경 위의 색깔
                foregroundColor: Colors.white,
                disabledForegroundColor: Colors.green, // 비활성화 시 글자색
                /// 그림자 색깔
                shadowColor: Colors.blue,
                elevation: 10,
                textStyle: TextStyle(
                  fontSize: 20,
                  fontWeight: FontWeight.bold,
                ),
                padding: EdgeInsets.all(20), /// 버튼 안의 텍스트와 버튼의 경계 사이의 간격
                side: BorderSide(
                  /// 버튼의 테두리
                  color: Colors.black,
                  width: 12, /// 4.0이 기본
                ),
                // minimumSize: Size(200, 50), /// 최소 크기
                // maximumSize: Size(200, 50), /// 최대 크기
                fixedSize: Size(200, 150), /// 고정 크기
              ),
              child: Text("Elevated Button"),
            ),
```
- OutlinedButton이랑 TextButton도 만약 같은 설정을 넣어주면 완전 같다!.
- 그래서 각 버튼들을 디자인하기 편하도록 초기 세팅이 되어 있는 프로토타입이라고 생각하면 편함.

## MaterialState.all()
- MaterialState
	 - hovered : 호버링 상태 (마우스가 버튼 위에 있을 때)  
		- 단, 마우스 호버링은 웹에서만 동작  
	- focused : 포커스 상태 (텍스트 필드)  
	 - pressed : 눌렀을 때 (0)  
	 - draged : 드래그 됐을 때  
	 - selected : 선택된 상태(체크밗, 라디오버튼)  
	 - scrollUnder : 다른 컴포넌트 밑으로 스크롤링 됐을 때.  
	 - disabled : 비활성화 상태 (0)  
	 - error : 에러 상태
```dart
OutlinedButton(  
  onPressed: (){},  
  style: ButtonStyle( 
    backgroundColor: MaterialStateProperty.all(  
      Colors.blue,  
    ),  
    minimumSize: MaterialStateProperty.all(  
      Size(200, 50),  
    ),  
  ),  
  child: Text("Outlined Button"),  
),
```
- MaterialState.all()
	- ButtonStlye 위젯 내 존재.
	- 기존에 사용하던 방식
	- `MaterialState.all()` => `MaterialState` 가 어떤 상태이던지 항상 다음과 같은 상태를 유지해라~
- 여기서 StyleFrom => 사실 ButtonStyle을 반환하는 함수임 ㅋㅋ

## MaterialState.resolveWith
```Dart
TextButton(  
  onPressed: () {},  
  style: ButtonStyle(  
    backgroundColor: MaterialStateProperty.resolveWith(  
        (Set<MaterialState> states) {  
      if (states.contains(MaterialState.pressed)) {  
        return Colors.amber;  
      }  
      return Colors.green;  
    }),  
    foregroundColor: MaterialStateProperty.resolveWith(  
      (Set<MaterialState> states) {  
        if (states.contains(MaterialState.pressed)) {  
          return Colors.red;  
        }  
        return Colors.black;  
      },  
    ),  
  ),  
  child: Text("Text Button"),  
),
```
- resolveWith 에는 파라미터로 콜백 함수가 들어와야 함.
- 위와 같이 콜백 함수를 넣으면 된다.

## Shape Of Button
- 아래 내용은 `elevated button`, `outlined button` `textbutton` 모두 동일.

- 기본 적용 방법
```Dart
OutlinedButton(  
  onPressed: (){},  
  style: OutlinedButton.styleFrom(  
    shape: StadiumBorder(),  
  ),  
  child: Text("Outlined Button ; For Shape"),  
)
```
- 이제 여기서 shape 파라미터 값만 변경
	- StadiumBorder -> 축구 경기장 모양(Default)
	- RoundedRectangleBorder()
		- 직사각형 ~> 둥글 축구 경기장 모양
		- borderRadius 파라미터 값에 따라서!
		- `RoundedRectangleBorder(borderRadius:BorderRadius.circular(20),  ),`
	- BeveledRectangleBorder
		- RoundedRectangleBorder 랑 똑같은 매개 변수 존재
		- 해당 매개 변수 값 따라 변화
	- ContinuousRectangleBorder
		- RoundedRectangleBorder 랑 똑같은 매개 변수 존재
		- 해당 매개 변수 값 따라 변화
	- CircleBorder
		- 원!
		- 내부 ecentricity 파라미터 : 0 ~ 1
		- 0은 원형 ~ 1은 럭비공

## IconButton
```Dart
ElevatedButton.icon(  
  onPressed: () {},  
  icon: Icon(Icons.keyboard),  
  label: Text("Elevated Button with Icon"),  
),
```
- 나머지 버튼 타입도 동일
- style 적용도 동일.
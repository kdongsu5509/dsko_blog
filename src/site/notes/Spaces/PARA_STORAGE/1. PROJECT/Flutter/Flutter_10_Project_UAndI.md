---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-10-project-u-and-i/"}
---

# 15. U&I 우리 사귄지 몇일
- DateTime
- MediaQuery
- DatePicker
- 여러개의 위젯으로 분리
- 폰트 적용
- 테마 사용

## 폰트 에셋 파일 추가
- Google Font와 같은 사이트에서 찾아서 사용!


## 레이아웃 작업하기
- SafeArea : Scaffold 내에 위치 -> 화면 정보를 바탕으로 가려지는 위젯 없도록 해줌 -> 화면 벗어나지 않게 해주는 건 당연.
- MediaQuery : 디바이스 미디어에 대한 정보 제공(화면 크기 등)

## 디자인 마무리하기
Colors.pink[] // 100~900 : 낮을 수록 밝음
Text 위젯의 style : 스타일 지정 가능.
	-폰트 패밀리(이름, 문자열), 크기, 색상 등등 가능.


## 테마 적용해보기
- 직관성 좋게 유지
MaterialApp 위젯에서 `theme` 파라미터 사용
- textTheme, buttonTheme 등 존재.
	- 가이드 라인은 없음. 적절히 잘 사용할 것. -> 협업할 때 특히.


적용 : style: Theme.of(context).textTheme.테마이름.

## DatePicker 사용해보기
```dart
IconButton(  
  iconSize: 60,  
  color: Colors.red,  
  onPressed: () {  
    showCupertinoDialog(  
      context: context,  
      // Dialog 밖 클릭 시 닫히는 코드
      barrierDismissible: true,  
      builder: (BuildContext context) {  
        return Align( // 정렬이 없으면 전체 사이즈 차지함.  
          alignment: Alignment.center,  
          child: Container(  
            color: Colors.white,  
            height: 300,  
            child: CupertinoDatePicker(  
			  //Container로 공간 확보 후 child로 DatePicker 사용
              mode: CupertinoDatePickerMode.date,  
              //CupertinoDatePicker가 필요로 하는 핵심 파라미터
              //이것 역시 IDE에서 확인 후 추가함.
              onDateTimeChanged: (DateTime value) {  
                print(value);  
                // onDateTimeChanged : 반환함수
                // 이것도 부모 위젯에서 파악.
              },  
              dateOrder: DatePickerDateOrder.ymd,  // 입력 순서 변경
            )  
          ),  
        );  
      },  
    );  
  }
```
- Cupertion : 애플 본사 위치 : 그래서 애플 관련 위젯에는 `cupertino` 가 들어감.
- showCupertinoDialog까지만 생각해내고 다 부모 위젯을 보고 작성한 코드들
	- 이렇게 하지 않으면 코드를 작성할 수 가 없다. -> 위젯이 너무 많아..
- 원칙을 이해하고 직접 돌려보면서(build 된 코드의 변경인 경우에는 hot reload를 하면서 코드 작성해야함.

---
## 상태 상위로 올리기
- 차후 유지보수를 위해서 중요
- 상태관리 툴을 사용하지 않고, 플러터 기본만 사용될 경우.
	- 공통인 부분에서 관리하는 것이 가장 좋음.
	- 하나의 묶음이 될만한 가장 공통적인 부분에서 하는 것이 정석!
- 상위 부분에서 특정 변수를 관리하게 되면 하위 부분에서 해당 변수를 사용하기 위해선 변수 호출 방법을 변경해야함. -> StatefulWidget에서!
	- 라이프사이클 때문에.
	- steateFul위젯은 createSet()함수를 통해 state 객체 생성.
	- 해당 변수는 stateFul위젯에서 관리하지만, 그것을 변경하는 부분은 state에 존재. 따라서 widget.변수명 같은 방식으로 호출해야함.
	- 즉 매커니즘은 아래와 같음.
		- 상위 위젯 A에서 관리.
		- 하위 위젯이자 stateful위젯인  B 호출 시 A에서 관리중인 변수를 파라미터로 전달.
		-  stateful위젯에서 값을 받았지만 state와는 엄연히 다른 객체. 그러나, 이를 이용해 state관리는 state위젯에서 실시됨.
		- 따라서 state위젯에서 사용 시에는 widget.변수명으로 불러야 함!

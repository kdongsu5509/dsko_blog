---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-12-alignment/"}
---

# 17. Alignment
- 정렬에 관하여.

- Base ; Container의 정렬 -> Scaffold가 좌상단에 배치함. -> 이것도 해당 코드가 실행될 OS에 따라서 다른 결과를 나타내기도 함.
```dart
void main() {  
  runApp(  
    MaterialApp(  
      home: Scaffold(  
        body: Container(  
          height: 300,  
          width: 300,  
          color: Colors.red,  
        ),  
      ),  
    ),  
  );  
}
```

- Center ; Center 위젯을 이용한 가운데 정렬
```dart
void main() {  
  runApp(  
    MaterialApp(  
      home: Scaffold(  
        body: Center(  
          child: Container(  
            height: 300,  
            width: 300,  
            color: Colors.red,  
          ),  
        ),  
      ),  
    ),  
  );  
}
```

- 세부 정렬1. Align 위젯 이용
```Dart
void main() {  
  runApp(  
    MaterialApp(  
      home: Scaffold(  
        body: Center(  
          child: Container(  
            height: 300,  
            width: 300,  
            color: Colors.red,  
            child: Align(  
              alignment: Alignment.center,
              /// center 말고도 다수 존재.
              child: Container(  
                height : 50,  
                width : 50,  
                color: Colors.blue,  
              ),  
            ),  
          ),  
        ),  
      ),  
    ),  
  );  
}
```

- 세부 정렬 2. x,y 좌표 지정
	- Align 위젯 내부에서 Alignment위젯 내 파라미터 이용
```dart
void main() {  
  runApp(  
    MaterialApp(  
      home: Scaffold(  
        body: Center(  
          child: Container(  
            height: 300,  
            width: 300,  
            color: Colors.red,  
            child: Align(  
              alignment: Alignment(  
                0.5,  
                0.5,  
              ),  
              child: Container(  
                height: 50,  
                width: 50,  
                color: Colors.blue,  
              ),  
            ),  
          ),  
        ),  
      ),  
    ),  
  );  
}
```

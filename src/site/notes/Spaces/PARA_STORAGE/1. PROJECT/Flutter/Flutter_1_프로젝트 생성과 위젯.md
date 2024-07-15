---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-1/"}
---

```toc
```

### 프로젝트 생성
- SDK 파일 조심
- 프로젝트 생성 폴더 조심.

### 에뮬레이터
- WINDOW에서는 ANDROID만 실행 가능.
	- 그런데 에뮬레이터 돌리면 보통 PIXEL 폰 사용.


### 살펴볼 코드
```Dart
import 'package:flutter/material.dart';

void main() {
  /// Run the app
  runApp(
    /// MaterialApp은 항상 최상위에 위치한다
    ///Scaffold는 바로 아래에 위치한다
    ///Widget : UI를 구성하는 요소
    MaterialApp(
      //MaterialApp : Material Design을 적용시킴
      debugShowCheckedModeBanner: false, // 디버깅 배너 제거
      home: Scaffold(
        // Scaffold : 화면 골조 형성
        backgroundColor: Colors.black,
        body: Center(
          child: Text(
            'Code Factory',
            style: TextStyle(
              color: Colors.white,
            ),
          ),
        ),
      ),
    ),
  );
}
```

### 구조
- MaterialApp : Material Design 적용
	- 구글이 제창하여 2014년부터 사용되기 시작한 플랫 디자인 기반의 디자인 시템.
- Scaffold : 화면 내부 구조 (뼈대) \
- 그 위로 더 다양한 위젯들이 존재 가능!

**위젯 : Flutter에서 UI를 구성하는 요소 **
- flutter의 materialApp이랑 scaffold도 위젯임!! -> 역할은 위젯마다 천지차이!

### Dart Format
- 왜 다른 언어라면 `,`를 사용하지 않는 곳에도 `,` 를 사용할까?
	- -> 다 Dart Format.

-> Flutter는 다양한 위제들이 하나의 화면을 이룸. 
-> 컴퓨터는 괄호를 이용해서 구분 가능. 하지만 프로그래머가 보기에는 힘들다!
-> 프로그래머가 보기 편하게 자동으로 정리 해줌 -> Dart Format으로!! 정리
단축키 : `Ctrl` + `Alt` + `L`

-> **정리 기준 : `,` **
	그래서 `,`를 사용.  미사용시 큰 상관은 없으나 보기 편하게 format할 수 없을 뿐.
---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-19-future-builder-and-stream-builder/"}
---

19 . FutureBuilder와 Stream
```dart
import 'package:flutter/material.dart';  
import 'dart:math';  
  
class homeScreen extends StatelessWidget {  
  const homeScreen({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    return Scaffold(  
      body: StreamBuilder<int>(  
        stream: streamNumbers(),  
        builder: (BuildContext context, AsyncSnapshot<int> snapshot) {  
          if(snapshot.hasError){  
  
          }  
  
          if(snapshot.hasData){  
            final data = snapshot.data;  
  
            return Center(  
              child: Text('Random number: $data'),  
            );  
          }  
  
          return Center(  
            child: Text('데이터가 없음'),  
          );  
        },  
  
      ),  
    );  
  }  
  
  Future<int> getNumber() async {  
    await Future.delayed(Duration(seconds: 1));  
  
    final random = Random();  
  
    throw Exception('에러가 발생했습니다.');  
  
    return random.nextInt(1000);  
  }  
  
  Stream<int> streamNumbers() async* {  
    for(int i = 0 ; i < 10 ; i++){  
      await Future.delayed(Duration(seconds: 1));  
      yield i;  
    }  
  }  
}
```
- 상위 빌더가 재실행 되면 FutureBuilder도 재실행  
	-  만약 실행 기록이 있다면, 데어터가 캐싱됨.  
	-  Future의 상태가 변할 때 마다 매번 다시 build 
		- ConnectionState.none: 아직 Future 또는 stream이 실행되지 않은 상태  
		- ConnectionState.active: stream에서만 존재, 스트림 아직 실행중  
		- ConnectionState.waiting: 실행중  
		- ConnectionState.done: Future 또는 stream이 종료된 상태   

---

`async`와 `async*`는 둘 다 Dart에서 비동기 프로그래밍을 지원하는 키워드이지만, 그 용도와 동작 방식은 다릅니다. 여기서는 두 키워드의 차이점을 설명합니다.

### `async`
- `async` 키워드는 비동기 함수임을 나타냅니다. 이 함수는 `Future`를 반환하며, `await` 키워드를 사용하여 비동기 작업이 완료될 때까지 기다릴 수 있습니다.
- `async` 함수는 비동기 작업을 수행하고 그 결과를 반환하는 데 사용됩니다.

#### 예제
```dart
Future<int> fetchData() async {
  await Future.delayed(Duration(seconds: 1));  // 1초 대기
  return 42;  // 결과 반환
}
```

이 함수는 1초 후에 42를 반환합니다. `await` 키워드는 비동기 작업이 완료될 때까지 기다립니다.

### `async*`
- `async*` 키워드는 비동기 생성자를 나타냅니다. 이 생성자는 `Stream`을 반환하며, `yield` 키워드를 사용하여 스트림의 항목을 하나씩 내보낼 수 있습니다.
- `async*` 함수는 비동기적으로 데이터를 스트림으로 생성하는 데 사용됩니다.

#### 예제
```dart
Stream<int> streamNumbers() async* {
  for (int i = 0; i < 10; i++) {
    await Future.delayed(Duration(seconds: 1));  // 1초 대기
    yield i;  // 스트림에 숫자 생성
  }
}
```

이 함수는 0부터 9까지의 숫자를 1초 간격으로 스트림에 내보냅니다. `yield` 키워드는 스트림 구독자에게 값을 전달합니다.

### 차이점 요약
- **반환 타입**:
  - `async`: `Future<T>`를 반환합니다.
  - `async*`: `Stream<T>`를 반환합니다.
  
- **사용 키워드**:
  - `async`: 비동기 작업을 기다릴 때 `await`를 사용합니다.
  - `async*`: 스트림에 값을 전달할 때 `yield`를 사용합니다.
  
- **용도**:
  - `async`: 비동기 작업을 순차적으로 수행하고 그 결과를 반환하는 함수에 사용됩니다.
  - `async*`: 비동기적으로 값을 생성하고 스트림을 통해 구독자에게 전달하는 함수에 사용됩니다.

### 실제 사용 예제

#### `async` 예제
```dart
Future<void> printData() async {
  int data = await fetchData();
  print(data);  // 42 출력
}

Future<int> fetchData() async {
  await Future.delayed(Duration(seconds: 1));
  return 42;
}
```

#### `async*` 예제
```dart
void printStreamData() async {
  await for (int value in streamNumbers()) {
    print(value);  // 0, 1, 2, ..., 9 출력
  }
}

Stream<int> streamNumbers() async* {
  for (int i = 0; i < 10; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}
```

위 예제에서는 `printStreamData` 함수가 `streamNumbers` 스트림을 구독하고, 1초마다 새로운 값을 출력합니다. `await for` 구문을 사용하여 스트림을 순차적으로 처리합니다.


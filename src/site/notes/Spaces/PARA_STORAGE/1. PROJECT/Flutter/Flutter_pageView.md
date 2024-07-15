---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-page-view/"}
---

`PageView`는 Flutter에서 수평 또는 수직으로 페이지를 전환할 수 있는 위젯입니다. 이는 주로 화면 슬라이드, 튜토리얼 화면, 이미지 갤러리 등의 구현에 사용됩니다. `PageView`는 여러 페이지를 자식으로 가지고 있으며, 사용자가 스와이프 제스처를 통해 페이지를 넘길 수 있도록 합니다.

### 기본 사용법

`PageView`의 기본적인 사용법은 매우 간단합니다. `PageView` 위젯은 `children` 속성을 사용하여 여러 페이지를 정의할 수 있습니다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('PageView Example'),
        ),
        body: PageView(
          children: [
            Container(
              color: Colors.red,
              child: Center(
                child: Text(
                  'Page 1',
                  style: TextStyle(fontSize: 24, color: Colors.white),
                ),
              ),
            ),
            Container(
              color: Colors.green,
              child: Center(
                child: Text(
                  'Page 2',
                  style: TextStyle(fontSize: 24, color: Colors.white),
                ),
              ),
            ),
            Container(
              color: Colors.blue,
              child: Center(
                child: Text(
                  'Page 3',
                  style: TextStyle(fontSize: 24, color: Colors.white),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

이 예제는 세 개의 페이지를 포함한 `PageView`를 생성합니다. 각 페이지는 서로 다른 배경색과 텍스트를 가지고 있습니다.

### 주요 속성

- **children**: 페이지로 표시될 위젯들의 리스트입니다.
- **controller**: `PageController`를 사용하여 페이지를 제어할 수 있습니다.
- **scrollDirection**: 페이지 전환의 방향을 설정합니다. 기본값은 수평 방향(`Axis.horizontal`)이며, 수직 방향(`Axis.vertical`)으로도 설정할 수 있습니다.
- **onPageChanged**: 페이지가 변경될 때 호출되는 콜백 함수입니다.

### PageController

`PageController`를 사용하면 프로그래밍적으로 페이지를 전환하거나 현재 페이지의 상태를 관리할 수 있습니다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: PageViewExample(),
    );
  }
}

class PageViewExample extends StatefulWidget {
  @override
  _PageViewExampleState createState() => _PageViewExampleState();
}

class _PageViewExampleState extends State<PageViewExample> {
  PageController _pageController = PageController();
  int _currentPage = 0;

  @override
  void dispose() {
    _pageController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('PageView Example'),
      ),
      body: Column(
        children: [
          Expanded(
            child: PageView(
              controller: _pageController,
              onPageChanged: (int page) {
                setState(() {
                  _currentPage = page;
                });
              },
              children: [
                Container(
                  color: Colors.red,
                  child: Center(
                    child: Text(
                      'Page 1',
                      style: TextStyle(fontSize: 24, color: Colors.white),
                    ),
                  ),
                ),
                Container(
                  color: Colors.green,
                  child: Center(
                    child: Text(
                      'Page 2',
                      style: TextStyle(fontSize: 24, color: Colors.white),
                    ),
                  ),
                ),
                Container(
                  color: Colors.blue,
                  child: Center(
                    child: Text(
                      'Page 3',
                      style: TextStyle(fontSize: 24, color: Colors.white),
                    ),
                  ),
                ),
              ],
            ),
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: List.generate(3, (index) {
              return Container(
                margin: EdgeInsets.all(4.0),
                width: 12.0,
                height: 12.0,
                decoration: BoxDecoration(
                  shape: BoxShape.circle,
                  color: _currentPage == index ? Colors.blue : Colors.grey,
                ),
              );
            }),
          ),
        ],
      ),
    );
  }
}
```

### 주요 구성 요소

1. **PageView**: 페이지 뷰를 생성합니다.
2. **PageController**: 페이지 뷰를 제어합니다.
3. **onPageChanged**: 페이지가 변경될 때 호출되는 콜백을 사용하여 현재 페이지를 업데이트합니다.
4. **현재 페이지를 나타내는 인디케이터**: `_currentPage`를 사용하여 현재 페이지를 추적하고, 이를 바탕으로 인디케이터를 업데이트합니다.

### 정리

`PageView`는 Flutter에서 페이지 전환을 쉽게 구현할 수 있는 강력한 위젯입니다. `PageController`를 사용하여 프로그래밍적으로 페이지를 전환하거나 페이지 상태를 관리할 수 있습니다. 이를 활용하면 다양한 페이지 기반의 UI를 쉽게 구성할 수 있습니다.
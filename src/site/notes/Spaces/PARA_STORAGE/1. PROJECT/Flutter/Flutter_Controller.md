---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-controller/"}
---

Flutter에서 컨트롤러는 다양한 위젯과 함께 사용되어 상태나 동작을 제어하는 데 중요한 역할을 합니다. 컨트롤러는 주로 텍스트 입력, 스크롤, 페이지 뷰 등과 관련된 위젯에서 사용됩니다. 여기서는 몇 가지 주요 컨트롤러와 그 사용법을 설명하겠습니다.

### 1. TextEditingController

`TextEditingController`는 텍스트 입력 필드 (`TextField`나 `TextFormField`)의 텍스트를 제어하는 데 사용됩니다. 이를 통해 텍스트를 읽거나 설정하고, 텍스트 변경 이벤트를 감지할 수 있습니다.

#### 예제:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TextControllerExample(),
    );
  }
}

class TextControllerExample extends StatefulWidget {
  @override
  _TextControllerExampleState createState() => _TextControllerExampleState();
}

class _TextControllerExampleState extends State<TextControllerExample> {
  TextEditingController _controller = TextEditingController();

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('TextEditingController Example'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
            ),
            ElevatedButton(
              onPressed: () {
                print('Current text: ${_controller.text}');
                _controller.text = 'Updated Text';
              },
              child: Text('Update Text'),
            ),
          ],
        ),
      ),
    );
  }
}
```

### 2. ScrollController

`ScrollController`는 스크롤 가능한 위젯 (`ListView`, `SingleChildScrollView` 등)의 스크롤 동작을 제어하는 데 사용됩니다. 이를 통해 스크롤 위치를 얻거나 설정하고, 스크롤 이벤트를 감지할 수 있습니다.

#### 예제:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ScrollControllerExample(),
    );
  }
}

class ScrollControllerExample extends StatefulWidget {
  @override
  _ScrollControllerExampleState createState() => _ScrollControllerExampleState();
}

class _ScrollControllerExampleState extends State<ScrollControllerExample> {
  ScrollController _controller = ScrollController();

  @override
  void initState() {
    super.initState();
    _controller.addListener(() {
      print('Scroll Position: ${_controller.position}');
    });
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('ScrollController Example'),
      ),
      body: ListView.builder(
        controller: _controller,
        itemCount: 50,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text('Item $index'),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          _controller.animateTo(
            0.0,
            duration: Duration(seconds: 2),
            curve: Curves.easeInOut,
          );
        },
        child: Icon(Icons.arrow_upward),
      ),
    );
  }
}
```

### 3. PageController

`PageController`는 `PageView`의 페이지 전환을 제어하는 데 사용됩니다. 이를 통해 현재 페이지를 얻거나 설정하고, 페이지 변경 이벤트를 감지할 수 있습니다.

#### 예제:

```dart
import 'package:flutter/material.dart';
import 'dart:async';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  Timer? timer;
  PageController controller = PageController();

  @override
  void initState() {
    super.initState();

    timer = Timer.periodic(
      Duration(seconds: 2),
      (timer) {
        int currentPage = controller.page?.toInt() ?? 0;
        int nextPage = currentPage + 1;
        if (nextPage > 4) {
          nextPage = 0;
        }

        controller.animateToPage(
          nextPage,
          duration: Duration(milliseconds: 300),
          curve: Curves.linear,
        );
      },
    );
  }

  @override
  void dispose() {
    timer?.cancel();
    controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: PageView(
        controller: controller,
        children: [1, 2, 3, 4, 5]
            .map((e) => Image.asset(
                  'asset/img/image_$e.jpeg',
                  fit: BoxFit.cover,
                ))
            .toList(),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: HomeScreen(),
  ));
}
```

### 요약

Flutter에서 컨트롤러는 다양한 위젯의 동작과 상태를 제어하는 데 중요한 역할을 합니다. 위의 예제들에서는 텍스트 입력, 스크롤, 페이지 전환을 제어하기 위해 각각 `TextEditingController`, `ScrollController`, `PageController`를 사용하는 방법을 보여주었습니다. 각 컨트롤러는 해당 위젯의 동작을 보다 정밀하게 제어하고 관리할 수 있도록 도와줍니다.
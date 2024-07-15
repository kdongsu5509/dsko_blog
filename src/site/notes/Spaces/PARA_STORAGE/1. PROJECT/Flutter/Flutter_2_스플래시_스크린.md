---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-2/"}
---

```toc
```

### YAML 구조
- YAML : JSON 포맷 불편함 해소 위해 만들어진 superset.
	- 일종의 데이터 직렬화 언어
	- 설정 파일, 데이터 전송 형식으로 주로 사용
	- 들여쓰기를 통해 계층 구조 표현
- 이것으로 DART 패키지를 관리 -> at the pubspec.yaml

##### yaml문법
###### key-value pair
```yaml
name : Code Factory
age : 32
gender : Male
```
- 아래와 동일
```dart
{
	'name' : 'Code Factory',
	'age' : 32,
	'gender' : 'Male'
}
```

###### List
```yaml
ive_members:
  - Yujin
  - Wonyoung
  - Rei
  - GaEul
  - ESeo
```
- 아래와 동일
```dart
{
 `ive_members` : [
	 'Yujin',
	 'WonYoung',
	 'Rei',
	 'GaEul',
	 'Eseo'
 ]
}
```
- 이후 중첩 시에도 위의 `-`, 와 들여쓰기만 잘하면 된다!.
- 주석은 `#` 이후에 작성하는 모든 것
---

### Asset 이미지 등록 및 사용
###### 등록
- 프로젝트 폴더 내에 `asset` 이라는 폴더 생성 후 그곳에 사진 저장.
	- (사진을 프로젝트 폴더에 저장해놓고 사용하는 경우)
- `pubspec.yaml` 에 주석 중 `assets` 찾기
	- 이미지 위치 설정 -> 사진은 ~~ 에 있어!라고 알려주기
```yaml
flutter:
# 앞에 2칸 들여쓰기
  uses-material-design: true

# 2칸씩 들여쓰고, `-` 다음에는 한 칸 띄우기.
  assets:
    - asset/img/ #asset 위치!
```
- 이후 `Pub get` 버튼 클릭하여 적용시키기.

###### 사용
```Dart
void main() {
	runApp(
		MaterialApp(
			home: Scaffold(
				body: Image.asset(에셋_주소);
			),
		),
	)
}
```
- Scaffold 위젯 내에서 setting.
- `image.asset` 말고도 다양한 image 하위 존재 => 상황에 맞제 사용할 것.
- ---

### HEXcode 색상 사용법
```dart
backgroundColor : Colors.red() 
///이렇게 안하여 더 자윧로를 높이는
```

```Dart
backgroundColor : Color(0xff112233);
```
- Color : 위젯 -> 16진수를 매개변수로 받음.
	- 0x : 이것은 16진수임을 나타내는 마크
	- ff -> 투명도
	- 112233 : 16진수 hex code

---
### column 위젯 사용법
- Scaffold의 body에 Column 사용 -> 위젯 여러 개 입력 가능
	- Column에는 child 대신 children 존재
		- children에는 아무거나 불가능!!! 정해진 것만!!!
---
### circularporgressindicator 위젯 사용법
- `CircularProgressIndicator` 위젯 : 로딩 애니메이션 제공 위젯
---
### statelessWidget 사용법
- statelessWidget : 다양한 위젯의 종류 중 1개
- 본인이 선언할 수도 있음! -> statelessWidget을 상속받은 자식 객체를 사용해서! 
	- Java의 다형성 처럼!!

- `stless` -> stateless 위젯을 간편하게 생성할 수 있는 단축어.

- 위젯 단위로 따로 빼놓아서 build()함수 안에 들어있음 -> Hot Reload 가능
	- 핫 리로드
		- **기본 정의** : 핫 리로드는 소스 코드의 변경 사항을 즉시 앱에 반영하되, 앱의 현재 상태를 **유지**하는 기능이다. 즉, 변수의 현재 값, 위젯 트리의 상태 등이 그대로 유지되면서 UI 변경 사항 또는 로직 변경 사항만 적용되는 것을 말한다.
		- **작동 원리** : Flutter는 Dart 언어를 사용하는데 이 Dart는 JIT(Just-In-Time) 컴파일을 지원한다. 핫 리로드는 이를 활용하여 변경된 소스 코드만 컴파일하고 앱에 즉시 반영할 수 있게 되는 것이다.
		- **적용하기** : UI의 디자인 변경, 로직 수정, 새로운 함수의 추가 등 대부분의 변경 사항에 적합하지만 다음 **제한 사항**과 같이 적용할 수 없는 부분도 존재한다.
		- **제한 사항** : '**main()**' 함수 내에 변경 사항, 전역 변수의 초기화 로직 변경, 앱의 전체적인 상태 초기화 로직등은 핫 리로드를 통해 반영되지 않기 때문에 핫 리스타트를 통해 반영해야 한다.
	- 핫 리스타드
		- **기본 정의** : 핫 리스타트는 앱을 처음부터 다시 시작하되, 앱을 재빌드하거나 재설치하지 않는 기능이다. 모든 앱 상태는 초기화되며(변수의 현재 값, 위젯 트리 상태 등), 앱은 처음부터 다시 시작된다.
		- **작동 원리** : 모든 위젯 트리와 상태는 초기화되며, 앱은 '**main()**' 함수부터 다시 실행되며, 처음 시작되는 화면으로 돌아간다.
		- **적용하기** : 앱의 초기화 로직 변경, 전역 변수의 변경, '**main()**' 함수 내의 변경 사항 등을 반영하고 싶을 때 사용된다.
		- **제한 사항** : 앱의 현재 상태와(메인 함수에 작성된 위치로) 메모리(기본 정의에 얘기한 것과 같이 변수나, 위젯 트리 상태 등의 값들)는 완전히 초기화된다.
	- 핫 리로드(Hot Reload)와 핫 리스타트(Hot Restart)의 핵심 차이점
		- **상태 유지**
			- **핫 리로드(Hot Reload)**는 앱의 현재 상태와 메모리를 유지한 채 변경 사항을 적용한다.
			- **핫 리스타트(Hot Restart)**는 앱의 모든 상태와 메모리를 초기화하고 앱을 처음부터 다시 시작한다.
		- **적용 범위**
			- **핫 리로드(Hot Reload)**는 대부분의 소스 코드 변경 사항을 즉시 반영할 수 있지만, 초기 앱 상태나 전역 변수의 변경은 반영되지 않는다.
			- **핫 리스타트(Hot Restart)**는 이러한 초기 상태 변경 사항까지 모두 반영하여 실행한다.

---
### padding 위젯 사용법
- Scaffold의 body에 padding 사용
	- 좌우 공백 세팅
```dart
body: Padding(
	padding: ~~~, //Padding에는 padding, 이 꼭 들어가야함.
	child : Column(~~~)
)
```
---
### sizedBox 위젯 사용법
- padding 보다 효율 굿
- SizedBox 사용 가능 하면 SizedBox 쓰기.
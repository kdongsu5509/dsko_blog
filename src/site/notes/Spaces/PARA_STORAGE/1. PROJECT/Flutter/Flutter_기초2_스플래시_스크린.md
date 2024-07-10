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

### 사용
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

### image 위젯 사용법
### column 위젯 사용법
### HEXcode 색상 사용법
### statelessWidget 사용법
### circularporgressindicator 위젯 사용법
### padding 위젯 사용법
### sizedBox 위젯 사용법
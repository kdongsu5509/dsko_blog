---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-5/"}
---

```toc
```
### 개념
- WebApp => WebSite을 볼 수 있는 Application

### Semantic Versioning
- 소프트웨어 버전 관리 방식 중 하나
- 버전 번호를 통해 소프트웨어의 변경 사항을 명확하게 전달하는 것이 목표

##### 버전 번호 형식
```DART
MAJOR.MINOR.PATCH
```
- MAJOR: 호환되지 않는 변경 사항이 있을 때 증가합니다.
- MINOR: 새로운 기능이 추가되지만, 이전 버전과 호환될 때 증가합니다.
- PATCH: 이전 버전과 호환되는 버그 수정이 있을 때 증가합니다.
##### 버전 증가 규칙
- MAJOR 버전: 기존 API와 호환되지 않는 변경이 있을 때, MAJOR 버전을 증가시킴.
	- 예를 들어, 기존 기능을 제거하거나 동작 방식을 변경하는 경우
- MINOR 버전: 기존 API와 호환되면서 새로운 기능을 추가할 때, MINOR 버전을 증가시킴. 
	- 예를 들어, 새로운 함수나 모듈을 추가하는 경우
- PATCH 버전: 기존 API와 호환되면서 버그를 수정할 때, PATCH 버전을 증가시킴
	-  예를 들어, 기존 기능의 버그를 수정하는 경우

##### Flutter에서 `^Major.Minor.Patch` 방식의 표기
- 의미
	- Major버전을 제외한 Update는 자동으로 하도록 설정.
- 이유
	- Major 업데이트의 경우 이전 버전과 호환되지 않음.
		- 따라서 개발자가 코드를 일부 변경시켜야 함. -> 주의가 필요
	- Minor, Patch 업데이트의 경우 이전 버전를 고려한 설계도 유효.
		- 따라서 자동으로 업데이트 설정해두어도 상관 없음.

---
### Pub.dev
- [PUB.DEV](https://pub.dev/)
- Dart와 Flutter 생태계에서 사용하는 패키지 관리 시스템
- 해당 페이지에서 외부 패키지 검색 및 다운로드 가능
	- 다운로드는 `pubspec.yaml`에서 depency setting 변경을 통해 가능
	- 이 때, yaml 문법 주의할 것.
- 각 패키지 별로 요구 사항이 다르니 꼭 읽어보기.
	-  예시
		- 안드로이드만, 혹은 ios 만, 혹은 모바일만 등등 지원하는 플랫폼의 차이
		- 플랫폼이 가능한 경우에도, 플랫폼별 설정이 다른 경우 존재.
			- 해당 경우, readme를 읽고 꼭 build.gradle 과 같은 설정 파일 변경해야함.
---
### AppBar 디자인하기
- AppBar : Scaffold(골조 형성 위젯)에 위치
- 역할 : 앱 상단에 위치하는 일종의 header 제작
```dart
Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.orange,
        title: Text("code factory"),
        centerTitle: true,
      )
```
- backgroundColor Default = > Colors.blue
	- 지정 시 해당 색상 우선 순위 가짐.
- centerTitle 
	- OS별 Default 다름
	- 통일하기 위해서는 지정해야함.

---
### WebView 초기화 하기
<div style="background : red"> 2024.07.11 22:09 까지 정리. 시간 없어서 차후로 미룸. </div>
<div style="background : red"> 추가적으로 rows, colums 그리고 padding 복습해야함. </div>


---
### 웹사이트 웹뷰에 띄우기 & 다큐멘테이션 읽어보기

---
### 콜백함수 이용해서 '홈으로' 버튼 만들어보기

---
### JavaScriptMode 변경하기

---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-0/"}
---



### 1. IDE 선택
- FLUTTER 개발에 사용하는 IDE
	- visual studio code
		- 그냥 관련 extention 들만 다운로드하면 가능.
		- 환경 세팅은 가장 편했음. 
		- 그러나 플러터에 최적화 된 환경이라고 생각이 들지는 않음.
			- emulator interface 가 구림.
		- 결론 : 세팅 간단히 하고 싶으면 이게 최고!
	- android studio.
		- 플러터 환경 최적화 되있는듯?
		- 대부분의 책이나 강의도 이 환경에 베이스를 두고 설명
		- 그러나 다운로드 시 주소에 반드시 '한글'이 있으면 안됨.
			- **윈도우 학생 계정으로 쓰시는 분들, 특히 조심하세요!!!**
		- 본인이 인텔리제이 IDE 를 경험한 적이 있으면 뭔가 친숙함.
		- 결론 : 최적화 되어있는 환경이 좋긴 하더라.. 근데 에러 뜨면 삭제하고 다시 차근차근 하다가 스트레스를 받기 좋았음.
	- intelliJ
		- Android studio 가 사실 인텔리제이 기반.
		- 인텔리제이에서 설정만 하면 잘 돌아감.
		- 관련 레퍼런스가 좀 적긴 하지만, 웬만하면 안드로이드 스튜디오랑 같아서 만약 IntelliJ를 사용하고 있다면... 뭐 굳이 설치할 필요 X
		- 결론 : 나는 이거씀... 안드로이드 스튜디오 오류 해결 귀찮아서 삭제하고, 인텔리이에 순응하기로...ㅎㅎ

### 2. Flutter SDK 설치
- [Flutter 설치 파일 주소-구글이 제공하는 공식 문서](https://docs.flutter.dev/get-started/install)
- 위의 주소에서 Flutter을 설치.
	-  **반드시 주소에 한국어가 들어가지 않는 곳** 에 해당 파일의 압축 해제본을 위치시키기!.
		- C드라이브에 그냥 `Flutter`라는 파일을 만든 후 그곳에 압축 해제하는 것을 강추!
	- 만약 한국어가 주소에 들어간다...?
		- 가상 휴대폰이 제대로 동작을 하지 않음...
			- 내가 작성한 코드가 모바일 환경에서 어떻게 돌아가는 지 확인을 하기 위해 가상의 모바일 환경(에뮬레이터)을 IDE에서 볼 수 있음.
			- 그런데 이게 작동이 안되어요ㅠ
				- The emulator process for AVD ＜에뮬레이터 이름＞ has terminated. 이라는 내용을 보여주는 창이 띄어짐과 동시에 안됨。
			- 나도 알고싶지 않았네요.



##### Additional
`The emulator process for AVD ~~~ has terminated` 에러 해결 과정

-  최초에 해당 문제를 CHATGPT를 이용해 해결하고자 했었음.
	- GPT가 주었던 해답.
		- AVD 설정에서 재설치 해봐.
		- Hypervisor 설정 확인해봐
		- HAXM 설치 확인 해봐.
		- 로그 확인해봐
		- 에뮬레이터 설정 변경해봐.

- AVD, HAXM 재설치
	- 재설치 해봤는데, 안되었음.

- 로그 및 에뮬레이터 설정 변경
	- 해당 환경 잘 몰라서 GPT와 대화하면서 진행.
	- 로그를 던져주니 Hypervisor 껐다가 다시 켜는 것을 추천함.

- 삼성 갤럭시 북 시리즈에서는 HYPERVISOR 끄는 것이 불가능하다고....
- [관련 삼성 커뮤니티 글](https://r1.community.samsung.com/t5/pc/%EC%82%BC%EC%84%B1-%EB%85%B8%ED%8A%B8%EB%B6%81-cpu%EA%B0%80%EC%83%81%ED%99%94-%EC%84%A4%EC%A0%95/td-p/22651503)


**내가 생각한 원인**
- 의도치않게 한글이 Flutter SDK 가 위치한 파일 주소에 포함되어있었음
	- -> 아마 윈도우 계정의 이름이 한글로 설정되어 있어서 바탕화면에 위치시키니 자연스 들어간 듯.
	- 윈도우 계정에서 이름을 변경할려고 하였는데, 윈도우 계정이 학교 이메일 연계 계정이라 사용자 이름 변경이 안되는 것으로 파악.
- Flutter SDK 와 Android Studio 환경으로 최초 세팅을 했었는데, 다 지우고 C드라이브에 flutter sdk만 새롭게 설치.
- IDE는 Android Studio-> IntelliJ로 변경
	- 이미 IntelliJ를 Ultimate로 사용하고 있었음 -> JetBrain이 학생이라고 무료로 제공 ㅠㅠ 사랑해요!!
	- Android Studio 파일이 생각보다 커서 기왕 있는 환경에 몇 가지만 추가해서 사용하자고 생각함.

-> 위의 방법으로 재설치 함으로써 해결.
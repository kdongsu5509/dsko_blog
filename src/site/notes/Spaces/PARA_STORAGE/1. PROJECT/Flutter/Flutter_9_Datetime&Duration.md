---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/flutter/flutter-9-datetime-and-duration/"}
---

# 14. DateTime & Duration
- DateTime : 날짜(with time)표현 클래스
```Dart
void main(){
 final date = Datetime(
	 1992, 11,23,1,23,25,30,5
 )
}
```
- 년,월,일,시,분,초,밀리 초, 마이크로 초에 해당 되는 값들을 순서대로 입력.
- 년도만 필수, 나머지는 옵션
	- 월, 일 기본값 : 1
	- 그 외 : 0
- 프로그램이 실행되는 시스템 시간 기준.

```Dart
void main(){
 final date = Datetime.utc(
	 1992, 11,23,1,23,25,30,5
 )

 final utcDate = date.toUtc();
 final LocalDate = utcDate.toLoacal();
}
```
- utc 기준 시간. -> 뒤에 'Z' 붙음

```dart
void main() {
	final now = Duration.now();
}
```
- 컴파일 된 기준의 시간.



- Duration : 기간 표현 클래스
```dart
void main() {
	final duration = Duration(
	days: 1
	hours : 1,
	minutes : 1,
	seconds : 1,
	milliseconds : 1,
	microseconds: 1,
	)
}
```
- Named Parameter로 날, 시, 분, 초 , 밀리 초, 마이크로 초 입력 가능
- 값을 입력하지 않으면  모든 값은 0으로 초기화됨.

```dart
void main() {
  final date = DateTime(
    1992, 11, 23,
  );
  
  final duration = Duration(
    days: 1
  );
  
  print(date.add(duration));
}
```

```dart
void main() {
  final ein = DateTime(
    1992,
    11,
    23,
  );

  final zwei = DateTime(
    2023,
    11,
    23,
  );

  print(ein.isAfter(zwei)); //false
  print(ein.isBefore(zwei)); //true
  //isAtSameMomentAs() 도 존재.
}

```

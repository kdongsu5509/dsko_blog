### 1. Form
`data_type? Name`
```C#
int? a = null;
float? b = null;
double? c = null;
```

### 2. Warning
`사용 이유 : 값 형식을 비워놓고 싶지만, 비워놓을 경우 컴파일 에러가 나서`
- 값 형식에서만 사용 가능. 참조 형식은 사용 불가

### 3. 속성
- HasValue : 해당 변수가 값을 갖고 있는지 또는 그렇지 않은지 나타냄
- Value : 변수에 담겨져 있는 값을 나타냄.
```C#
int? a = null;
Console.WriteLine(a.HasValue); //a는 null이라 False

a = 37;
Console.WritheLine(a.HasValue); //True
Console.WriteLine(a.Value); //37
```


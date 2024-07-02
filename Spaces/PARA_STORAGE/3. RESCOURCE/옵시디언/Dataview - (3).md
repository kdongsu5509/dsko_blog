---
aliases:
  - Dataview - (3)
tags:
  - obsidian
  - "#study"
sticker: emoji//1f7ea
---


![](https://blog.kakaocdn.net/dn/c4RVko/btrxc20481a/thzmaWXLYFBzKDFZJsBKwK/img.png)

### **시리즈**

[Obsidian 옵시디언, 원하는 정보만 쏙쏙 골라주는 Dataview - (1)](https://olait.tistory.com/23)

[Obsidian 옵시디언, 원하는 정보만 쏙쏙 골라주는 Dataview - (2)](https://olait.tistory.com/27)   
[Obsidian 옵시디언, 원하는 정보만 쏙쏙 골라주는 Dataview - (3)](https://olait.tistory.com/28)  

### **목차**

-   Dataview 쿼리문
    -   어떻게 표현할 것인가 (TABLE, LIST / TASK)
    -   무엇을 가져올 것인가 (Field)
    -   어디서 가져올 것인가 (FROM)
    -   어떤 조건을 만족시키는 것을 가져올 것인가 (WHERE)
    -   어떤 순으로 가져올 것인가? (SORT)

### **Dataview 쿼리문**

앞선 시리즈를 통해서 데이터뷰에서 어느정도 아셨을 거라고 가정하고 데이터뷰를 이용해서 원하는 정보만 쏙쏙 모아서 볼 수 있도록 쿼리문을 작성해봅시다! 일반적인 쿼리문 형태는 다음 코드블록과 같습니다.

````
```dataview
<span>TABLE</span><span>|</span>LIST<span>|</span>TASK <span>&lt;</span>field<span>&gt;</span> [<span>AS</span> "Column Name"], <span>&lt;</span>field<span>&gt;</span>, ..., <span>&lt;</span>field<span>&gt;</span> 
<span>FROM</span> <span>&lt;</span>source<span>&gt;</span> (<span>like</span> #tag <span>or</span> "folder")
<span>WHERE</span> <span>&lt;</span>expression<span>&gt;</span> (<span>like</span> <span>'field = value'</span>)
SORT <span>&lt;</span>expression<span>&gt;</span> [<span>ASC</span><span>/</span><span>DESC</span>] (<span>like</span> <span>'field ASC'</span>) 
```
<span>Copy</span>
````

데이터뷰에서 각 노트에 Annotation 된 정보를 가져오는 쿼리 언어입니다. 거창하지만 그렇게 거창하지 않습니다. SQL문을 작성해보신 분이라면 아주 쉽고 빠르게 이해하실 수 있습니다. 키워드인 **TABLE / LIST / TASK, FROM, WHERE, SORT** 만 사용하시면 됩니다. 각각은 다음과 같은 의미를 지니고 있습니다. 각 키워드 뒤에 오는 field, source, expression만 작성해서 우리가 원하는 정보만 가져올 수 있도록 하는 것입니다.

-   어떤 타입으로 표현할 것인가 (TABLE/LIST/TASK)
-   무엇을 가져올 것인가(Field)
-   어디서 가져올 것인가(FROM)
-   어떤 조건을 만족시키는 것만 가져올 것인가(WHERE)
-   어떤 순으로 가져올 것인가(SORT)

#### **어떻게 표현할 것인가(TABLE,LIST/TASK)**

가져온 데이터를 어떻게 표현할 지 선택합니다. 표와 리스트 그리고 태스크 방식이 있습니다. 이는 시리즈 - 1 편에서 알아보았기 때문에 넘어가도록 하겠습니다.

#### **무엇을 가져올 것인가(Field)**

TABLE reading AS "독서"  
Field는 키워드는 아니고 **TABLE** 형식으로 표현할 때 사용됩니다. 표의 열에 해당하는 것을 정하는 것입니다. 우리는 노트의 프론트매터(frontmatter)방식, 인라인 필드(Inline Fields) 그리고 내재된(Implicit Fields)를 선택할 수 있습니다. 예를 들어

````
```dataview
TABLE 
  reading <span>as</span> <span>"독서"</span>
  workout <span>as</span> <span>"운동"</span>
  ...(생략)
```
<span>Copy</span>
````

보관함의 어디서 가져올 것인가(FROM)에 만족하는 노트들에서 reading, workout필드를 찾아낼 것입니다. 두 가지 필드가 프론트매터, 인라인 필드에 존재한다면 데이터뷰는 그 정보를 표시할 것입니다. 만약에 특정 노트에만 존재한다면 해당 필드가 없는 노트들은 - 로 표시하게 됩니다. 아래 그림과 같이

![](https://blog.kakaocdn.net/dn/b6LWlm/btrq6uByRRO/ddaKKIPkDPpILo6N1mDMGk/img.png)

필드가 없으면 - 로 표시됩니다.

#### **어디서 가져올 것인가(FROM)**

데이터뷰는 자체적으로 보관함 내에 노트들, 노트 안에 작성된 할 일 목록, 태그 등을 빠르게 조회할 수 있도록 인덱싱이 되어있습니다. 즉 아래의 4개의 타입을 쿼리문 중 **FROM** 절 뒤에 작성을 합니다. 폴더 및 파일 경로는 ""로 감싸주세요

1.  태그 (예. FROM "#Planner")
2.  폴더 경로 (예. FROM "/Planner" - Planner 폴더 아래에 있는 모든 노트를 조회함)
3.  파일 경로 (예. FROM "/Planner/2022/01 Daily/2022-01-10" - 정확히 2022-01-10 노트 안의 내용에서만 조회)
4.  인, 아웃 링크
    1.  인링크 : 특정 노트를 참조한 노트들을 조회함 (예. FROM [Daily](file:///F:/Obsidian/ConnectingDots/Inbox/Daily.html))
    2.  아웃링크 : 특정 노트에서 참조한 노트들을 조회함 (예. FROM outgoing([Daily](file:///F:/Obsidian/ConnectingDots/Inbox/Daily.html)))

**예시**

```
<span>``</span><span>`dataview
LIST
FROM "/Planner"
`</span><span>``</span>
Copy
```

#### **어떤 조건을 만족시키는 것을 가져올 것인가(WHERE)**

예를 들어, 2022-01-01 이후에 만들어진 노트를 가져오고 싶다면 어떻게 해야할까요? 또는 오늘부터 2주 전에 수정된 노트에 대해서 가져오고 싶다면 어떻게 해야할까요? 바로 WHERE 키워드는 어떤 특정한 조건을 만족시키는 노트, 태스크들만 데이터뷰에서 조회할 수 있도록 하는 쿼리문입니다. 특히 조건에 해당하는 부분을 잘 다루면 다룰수록 우리가 원하는 정보만 더 잘 빼올 수 있습니다. 자바스크립트 기반이기 때문에 프로그래밍적인 요소가 강하지만 차근 차근 따라오시면 좋겠습니다.

**리터럴(Literal)**

자바스크립트에서는 리터럴이라는 개념이 있습니다. 리터럴이란 데이터 그 자체를 뜻하고 **변수에 넣지 않는 변하지 않는 데이터**라는 뜻을 가집니다. 이해하기 쉽도록 데이터뷰에서 사용할 수 있는 **재료**라고 생각하면 됩니다. 아래 표에서 보는 것과 같이 데이터뷰에서 사용할 수 있는 데이터 종류는 숫자, 불리언, 텍스트, 날짜, 기간, 링크, 리스트, 오브젝트 8가지로 되어있습니다. 오브젝트로 인해서 더 많은 요소들을 표현할 수 있지만 프로그래밍에 익숙하지 않다면 이런 게 있구나 정도로 넘어가시면 좋겠습니다. (_우리는 프로그래밍 언어를 배우는 게 아니라 옵시디언을 알아가는 것이니까요_)

<table data-ke-align="alignLeft" data-ke-style="style8"><tbody><tr><td><b>리터럴 종류</b></td><td><b>예시</b></td></tr><tr><td>숫자</td><td>1</td></tr><tr><td>불리언</td><td>true/fase</td></tr><tr><td>텍스트</td><td>"text"</td></tr><tr><td>날짜</td><td>date(2022-01-18)</td></tr><tr><td>기간</td><td>dur(1 day)</td></tr><tr><td>링크</td><td>[[Link]]</td></tr><tr><td>리스트, 배열</td><td>[1,2,3]</td></tr><tr><td>오브젝트</td><td>{a: 1, b:2}</td></tr></tbody></table>

리터럴 종류 중에 날짜와 기간은 자바스크립트의 함수이기 때문에 안의 내용에 따라서 좀 더 풍부하게 표현할 수 있습니다. 자세한 내용은 [Literals - Dataview (blacksmithgu.github.io)](https://blacksmithgu.github.io/obsidian-dataview/query/literals/) 에서 참조할 수 있습니다.

![](https://olait.tistory.com/Pasted%20image%2020220118231009.png)

![](https://blog.kakaocdn.net/dn/cBqNDE/btrq6Pk9U4W/fZjkswJaVsmPBXGwtyyLik/img.png)![](https://blog.kakaocdn.net/dn/HooLY/btrq7aWVVkL/omZ4kCd7QcknI9tARsi4v1/img.png)

date와 dur 함수 사용방법

**조건문 표현**

위에서 WHERE 키워드 뒤에 조건문에 쓸 수 있는 재료를 알아보았습니다. 그렇다면 재료들을 가지고 어떻게 조건문을 만들 수 있는 지 알아보겠습니다. 조건문을 표현할 때 재료들(리터럴)을 비교해서 다양한 조건을 만들어낼 수 있습니다. 결국 조건문의 결과는 조건을 모두 만족시킨 값들이라고 생각할 수 있습니다. 비교란 것은 부등호로 표현을 할 수 있습니다.

-   a > b
-   a < b
-   a = b
-   a != b
-   a <= b
-   a >= b

**예시**

```
file.ctime &gt; date(2022-01-18) - 파일이 만들어진 시간이 2022년 1월 18일보다 큰 파일을 가져와라.
file.path = "/Planner" - 파일 경로에 Planner가 있는 파일을 가져와라
```

#### **어떤순으로 가져올 것인가(SORT)**

마지막으로 SORT 키워드는 필드를 선택해서 오름차순 정렬(ASC) 또는 내림차순 정렬(DESC)를 합니다. 날짜 순으로 할 때에도 가장 최신의 데이터를 상위로 올리기 위해서는 내림차순 정렬로 하면 됩니다.

**예시**

````
```dataview
...(생략)
SORT start_read_date DESC 
```
````

다음 시리즈에서는 여러 가지 구체적인 예시를 살펴보면서 데이터뷰의 많은 예시를 통해서 이해를 돕도록 하겠습니다. 

---

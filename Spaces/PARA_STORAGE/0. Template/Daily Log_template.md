---
aliases:
  - For Daily Log
created date: 
tags:
  - dialyLog
sticker: lucide//calendar-days
---
### 0-0. Routine
- [ ] 08:30 구글 캘린더 확인 -> 오늘 할 일 확인(study 제외)
- [ ] study 내용 확인.
	- [[weekly plan]]
{{{{{{{{{하루 일과 후}}}}}}}}}
- [ ] 삼성 노트 내용 가져오기
- [ ] Study Data 정리
- [ ] 아래 dataview 날짜 바꾸기(date("YYYY-MM-DD")형식으로)
- [ ] 해밍웨이 다리 만들기

### 0-1. 짬짬이 체크리스트들.
- 프로젝트를 시작할 때 참고.
	- [[checkList_프로젝트 시작]]
- 오늘이 일요일이라면 아래 일 추가!
	- 달의 마지막 일요일인가? -> [[checkList_월간]] // [[checkList_주간리뷰]]
	- 아니라면 -> [[checkList_주간리뷰]]
- 일의 시작점을 모르겠으면 참고
	- ![[checkList_일할 때]]
### 1. Study Log
```dataview
list
from #study 
where file.cday = date(today)
```

### 2. Today Note
```dataview
list
where file.cday = date(today)
```

### 3. Diary(txt)



### 하루 마무리 checkList(해밍웨이 다리)
- [ ] 내일 할 일은 무엇인가
- [ ] 그 일들의 목표는 무엇인가
- [ ] 잊기 쉬운 세부 사항들이 있는가 / 있다면 무엇인가
- [ ] 피드백


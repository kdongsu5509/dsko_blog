---
{"dg-publish":true,"permalink":"/spaces/para-storage/pdf-with-pdfbox/"}
---



#### 문제 제기
PDF를 곧장 프린터기로 출력을 어떻게 할 수 있을까?

###### 상황.
- Spring 서버에서 PDF을 매개변수로 받아서 프린터기로 출력하고 싶음.
- 무료 api 사용 희망

##### 여러 가지 라이브러리 비교
1. JNA winspool
2. itextpdf
3. pdfbox

1. JNA winspool
	- 관련 블로그 기록이 거의 존재하지 않음. 있어도 영어 문서만 존재하여 참고하지 않음.
	- 공식문서를 보고 환경 설정을 해야 하는데, 환경 설정 코드 작성이 매우 복잡함.
2. itextpdf
	- 매우 좋음. 그러나 유료. 유료인 이유가 있다...(상용인 경우)
3. pdfbox
	- 사실 해당 문서도 공식 문서 제외하고 이러한 상황 아래에서 작성한 코드가 없었음.
	- 공식 문서를 보고 파악하기 에 다소 헷갈리는 부분 존재.

**- pdfbox 다소 헷갈리는 부분.**
-> Printable? 개꿀~ -> 근데 print함수에서 print 대상은 graphics임. 즉, img 파일임.
: 파일을 IMG로 변환 후 매개변수에 전달해야 함.
```Java
public interface Printable {

    //위에 생략
    int print(Graphics graphics, PageFormat pageFormat, int pageIndex)
                 throws PrinterException;

}
```

*다음 메서드 사용하여 코드 작성하여야 파일 자체 값을 byte[]로 전달하여 출력 가능*
```Java
public abstract class PrinterJob {
	    public void print(PrintRequestAttributeSet attributes)
        throws PrinterException {
        print();
    }
}
```
- PrintJob에서 Pageable 을 구현한 인스턴스를 던져줘야함.
- 그리고 PrintRequestAttributeSet을 설정하여 복사기 설정 가능.
- 이후 Print 함수 호출하면 Pageable을 구현한 인스턴스를 PrintRequestAttributeSet에 따라 출력.

- Pageable한 것을 본인이 출력하고자 하는 파일 타입에 따라 적용. -> 이미 구현되어 있으니 찾아서 적용만 하면 됨. 
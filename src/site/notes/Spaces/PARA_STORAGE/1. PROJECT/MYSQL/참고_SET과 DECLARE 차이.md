---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/mysql/set-declare/"}
---

`SET @변수명`과 `DECLARE 변수명 타입`
- 둘 다 변수 선언 및 초기화를 위해 사용
- 그 사용 목적과 문맥에서 차이.

### 1. `SET @변수명`:

- **사용 문맥**: 세션 변수 (Session variables)
- **사용 예**: 일반적인 SQL 문에서 전역적으로 사용할 때
- **선언과 초기화**: 한 줄에서 동시에 수행

#### 예시

```sql
-- 변수 선언 및 초기화 
SET @myVariable = 10;  
-- 변수 사용 
SELECT @myVariable;
```

- **특징**:
    - `SET`을 사용하여 변수의 값을 설정합니다.
    - 변수명 앞에 항상 `@`를 붙여야 합니다.
    - 이러한 변수는 세션 변수로, 현재 세션 동안 유지

### 2. `DECLARE 변수명 타입`:

- **사용 문맥**: 저장 프로시저, 트리거, 함수 내에서 지역 변수 (Local variables)
- **사용 예**: 저장 프로시저나 트리거 내에서 사용할 때
- **선언**: 별도의 `DECLARE` 문을 통해 수행
- **초기화**: `SET` 또는 `SELECT ... INTO` 문을 통해 수행

#### 예시
```SQL
DELIMITER $

CREATE PROCEDURE MyProcedure()
BEGIN
    -- 변수 선언
    DECLARE myVariable INT;
    
    -- 변수 초기화
    SET myVariable = 10;

    -- 변수 사용
    SELECT myVariable;
END $

DELIMITER ;
```

- **특징**:
    - 지역 변수를 선언할 때 사용합니다.
    - 선언된 변수는 프로시저, 트리거, 함수의 범위 내에서만 유효합니다.
    - 변수명 앞에 `@`를 붙이지 않습니다.

### 주요 차이점 요약

1. **문맥**:
    
    - `SET @변수명`: 일반적인 SQL 문에서 사용되며, 세션 변수로 선언됩니다.
    - `DECLARE 변수명 타입`: 저장 프로시저, 트리거, 함수 내에서 지역 변수로 선언됩니다.
2. **변수의 범위**:
    
    - `SET @변수명`으로 선언된 변수는 세션 전체에서 사용 가능합니다.
    - `DECLARE 변수명 타입`으로 선언된 변수는 선언된 블록(프로시저, 트리거, 함수) 내에서만 사용 가능합니다.
3. **초기화**:
    
    - `SET @변수명`: 선언과 동시에 초기화가 가능합니다.
    - `DECLARE 변수명 타입`: 선언 후 별도로 `SET`이나 `SELECT ... INTO`를 통해 초기화해야 합니다.

### 예시: `OUT_PROC` 저장 프로시저
```SQL
-- 테이블 생성
CREATE TABLE NOTABLE (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    TXT CHAR(10)
);

-- 프로시저 정의
DELIMITER $
CREATE PROCEDURE OUT_PROC(
    IN TXTVALUE CHAR(10),
    OUT OUTVALUE INT
)
BEGIN
    -- 변수 선언 및 초기화
    DECLARE maxID INT;

    -- 데이터 삽입
    INSERT INTO NOTABLE (TXT) VALUES (TXTVALUE);

    -- 변수에 값 할당
    SELECT MAX(ID) INTO maxID FROM NOTABLE;

    -- OUT 매개변수에 값 할당
    SET OUTVALUE = maxID;
END $
DELIMITER ;

-- 프로시저 호출
SET @output_value = 0;
CALL OUT_PROC('SampleText', @output_value);
SELECT @output_value;
```

이 예시에서:

- `DECLARE maxID INT;`는 `OUT_PROC` 프로시저 내에서 지역 변수 `maxID`를 선언합니다.
- `SET @output_value = 0;`은 세션 변수 `@output_value`를 선언하고 초기화합니다.
- 프로시저 내에서는 지역 변수를 사용하여 작업을 수행하고, 세션 변수를 통해 결과를 반환받습니다.
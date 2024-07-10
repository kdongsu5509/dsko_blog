---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project/mysql/sql-oldtable/"}
---

SQL에서 `OLD`와 `NEW`는 트리거(trigger)에서 사용되는 가상 테이블입니다. 이들은 트리거가 실행될 때 특정 작업에 대한 이전(OLD) 및 새로운(NEW) 데이터를 참조하는 데 사용됩니다.

### OLD 테이블

`OLD` 테이블은 트리거가 발생하기 전의 데이터를 포함하는 가상 테이블입니다. 일반적으로 이전에 수행되었던 `UPDATE` 또는 `DELETE` 작업에서 영향을 받는 레코드의 데이터를 담고 있습니다. 예를 들어, `UPDATE` 트리거에서 `OLD` 테이블은 업데이트 되기 전의 이전 값을 나타냅니다.

### NEW 테이블

`NEW` 테이블은 트리거가 발생한 후의 데이터를 포함하는 가상 테이블입니다. 주로 `INSERT` 또는 `UPDATE` 작업에서 새로 추가되거나 업데이트된 레코드의 데이터를 담고 있습니다. 예를 들어, `INSERT` 트리거에서 `NEW` 테이블은 새로 추가되는 레코드의 값을 나타냅니다.

### 사용 예제

다음은 `OLD`와 `NEW` 테이블이 어떻게 사용되는지 간단한 예제입니다:

1. **UPDATE 트리거에서의 OLD와 NEW**
    
    sql
    
    코드 복사
    
    `CREATE TRIGGER before_update_example BEFORE UPDATE ON ExampleTable FOR EACH ROW BEGIN     -- OLD 테이블을 사용하여 이전 값을 확인할 수 있음     IF OLD.column1 <> NEW.column1 THEN         INSERT INTO AuditTable (old_value, new_value)         VALUES (OLD.column1, NEW.column1);     END IF; END;`
    
    위의 예제에서 `BEFORE UPDATE` 트리거는 `ExampleTable`에서 레코드가 업데이트되기 전에 실행됩니다. `OLD.column1`은 업데이트되기 전의 `column1`의 값이고, `NEW.column1`은 업데이트된 후의 `column1`의 값입니다.
    
2. **INSERT 트리거에서의 NEW**
    
    sql
    
    코드 복사
    
    `CREATE TRIGGER after_insert_example AFTER INSERT ON ExampleTable FOR EACH ROW BEGIN     -- NEW 테이블을 사용하여 새로 추가된 데이터를 확인할 수 있음     INSERT INTO AuditTable (new_value)     VALUES (NEW.column1); END;`
    
    위의 예제에서 `AFTER INSERT` 트리거는 `ExampleTable`에 새로운 레코드가 추가된 후에 실행됩니다. `NEW.column1`은 새로 추가된 레코드의 `column1`의 값입니다.
    

### 요약

`OLD`와 `NEW` 테이블은 SQL 트리거에서 이전과 새로운 데이터에 접근할 수 있게 해주는 특별한 가상 테이블입니다. 이들을 사용하여 트리거에서 데이터 변경에 따른 추가적인 작업을 수행할 수 있습니다.
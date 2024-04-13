# MySQL에 배열 데이터를 저장
## 1. 정규화 (테이블 분리 & 관계)
데이터베이스에 배열을 그대로 하나의 레코드에 저장할 수는 없다. 왜냐하면 이는 제1정규형에 위반되므로 기본적으로 RDBMS에서 제한하기 때문이다. 

따라서 배열을 저장하는 테이블을 따로 만들고, 관계를 맺어 SELECT할 떄 JOIN을 하는 것이 FM이다. 
다만 JOIN은 DB에 부담가는 기능이기에 잦은 JOIN은 서비스 성능 저하로 연결된다. 

## 2. 배열 문자열 저장 
배열 자료형을 문자열로 변환한 뒤 그대로 테이블 스트링 칼럼에 저장한다. 

호출 시 문자열을 불러와 다시 파싱하여 배열 자료형을 만들어 사용한다. 

```javascript
// 자바스크립트에서 기본으로 지원하는 JSON 클래스를 이용해 간단하게 배열을 문자열로 그리고 다시 복구할 수 있다.

const arr = ['Apple', 'Banana', 'Orange']; 

let data = JSON.stringify(arr); // '["Apple","Banana","Orange"]' // 배열 문자열

let data2 = JSON.parse(data); // ['Apple', 'Banana', 'Orange'] 배열 자료형
```
> JSON() 클래스는 자바스크립트 객체를 변환하는 api지만, 사실 자바스크립트 배열도 객체의 일종이기 때문에 이런식으로 응용이 가능하다
## 3. MySQL에서 지원하는 JSON 타입 
MySQL Ver. 5.7.8부터 아예 JSON 데이터를 저장할 수 있게 필드 타입 기능을 지원한다. 객체 뿐만 아니라 배열 역시 지원한다.
보다 데이터베이스 테이블을 하드하게 관리하고 싶다면 고려해볼만 하다.

> 다만 JSON 필드는 데이터를 능동적이게 저장하게 하기 위한 옵션이지, 쿼리 성능 자체는 그냥 스트링 타입 컬럼에 저장하고 꺼내쓰는것이 더 빠르다.따라서 성능과 관리 두마리의 토끼를 잡기란 어려우므로 서비스 특성을 고려해서 잘 선택해야 한다.
```sql
CREATE TABLE example (
  `id` int NOT NULL AUTO_INCREMENT,
  `docs` JSON, -- json 타입 필드
  PRIMARY KEY (`id`)
);

INSERT INTO example (docs) VALUES ('["hot", "cold"]'); -- 배열 문자열을 저장
-- 그러면 배열이 테이블에 들어가게 된다.
```

### JSON 다른 활용 방법들 
```sql 
-- sql 쿼리 쓰듯이, string 입력을 할 수 있다.
INSERT INTO example(docs) VALUES ('{"a": "A", "b":"B"}');

-- json_object 형식으로 key, value 순서쌍으로도 입력 가능 
INSERT INTO example(docs) VALUES ('{"a", "A", "b", "B"}');

-- Error) json 내 항목을 배열 (list)로 입력할 땐 바로 할 수 없다.
INSERT INTO example(docs) VALUES ('{"a", "A", "[1, 2, 3]", "B"}');

--  json_array 형식을 사용해야 한다. 
INSERT INTO example(docs) VALUES (json_object("a", JSON_ARRAY(1,2,3), "b", "B"));
```


# REFERENCE
https://inpa.tistory.com/entry/MYSQL-%F0%9F%93%9A-RDB%EC%97%90-%EB%B0%B0%EC%97%B4%EC%9D%84-%EC%A0%80%EC%9E%A5%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95#thankYou

https://givemethesocks.tistory.com/75

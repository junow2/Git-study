## 파워셀에서 MySQL 실행하기
```
1. 해당 설치 풀더로 이동 
2. .\mysql.exe -uroot -p
```

## 데이터베이스 목록 확인 
```sql
show databases; 
```
## 데이터베이스 생성
```sql
create database [DB]; 
```
https://github.com/junow2/Self-study/blob/main/%5BMYSQL%5D%20Default%20DB.md
## 데이터베이스 삭제
```sql
drop database [DB];
```
## 데이터베이스 사용 
```sql
use [DB]; 
```
성공시 Databased Changed라는 문장이 출력된다. 
## 데이터베이스 내 테이블 목록 확인 
```sql
show tables;
```
## 테이블 생성하기 
```sql
CREATE TABLE testTable(                               (1)
  id INT(11) NOT NULL AUTO_INCREMENT,                 (2)
  name VARCHAR(20) NOT NULL,                          (3)
  ouccupation VARCHAR(20) NULL,                       (4)
  height SMALLINT,                                    (5)
  profile TEXT NULL,                                  (6)
  date  DATETIME,                                     (7)
  CONSTRAINT testTable_PK PRIMARY KEY(id)             (8)
);

(1) 테이블을 생성하는 명령어입니다.
(2) id라는 컬럼을 추가하는 데, INT 타입으로 지정합니다. NOT NULL은 값을 비워둘 수 없음을 의미합니다. AUTO_INCREMENT는 자동으로 값이 1씩 증가하도록 설정하는 옵션입니다.
(3) name이라는 컬럼을 추가하는데, 가변길이로 20글자까지 허용합니다. (20글자가 넘어가면 20글자에서 자릅니다.)
(4) 위와 동일하지만, 값을 비워두는 것을 허용합니다.
(5) SMALLINT는 INT보다 가질 수 있는 값의 범위가 작습니다. 메모리 측면에서 이득입니다.
(6) TEXT는 아주 긴 문자열을 취급할 때 사용합니다.
(7) DATETIME은 날짜와 시간에 관한 타입입니다.
(8) CONSTRAINT는 제약조건이라는 의미입니다. testTable의 PRIMARY KEY를 id 컬럼으로 지정하겠다는 의미이며, 이 제약조건의 이름을 testTable_PK로 지정한 것입니다.

Cf. CHECK : 값의 범위를 제한합니다.
    FOREIGN KEY : 다른 테이블과 JOIN할 때 사용합니다.
```

## 테이블 구조 확인하기 
```sql
DESC [TABLE]; 

-- 결과값 
+---------+-------------+------+-----+---------+----------------+
| Field   | Type        | Null | Key | Default | Extra          |
+---------+-------------+------+-----+---------+----------------+
| id      | int(11)     | NO   | PRI | NULL    | auto_increment |
| name    | varchar(50) | NO   |     | NULL    |                |
| height  | smallint(6) | YES  |     | NULL    |                |
| profile | text        | YES  |     | NULL    |                |
| date    | datetime    | YES  |     | NULL    |                |
+---------+-------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

```
# 테이블 값 변경하기 
## 1. 컬럼 추가 (ADD)
```sql
ALTER TABLE [TABLE] ADD COLUMN [컬럼명] [자료형]
```
```sql
-- EX. 
mysql> ALTER TABLE testTable
    -> ADD COLUMN release_date int(20) NOT NULL; -- 테이블 마지막으로 삽입

-- 테이블 맨 앞으로 삽입 
ALTER TABLE testTable ADD COLUMN release_date int(20) NOT NULL FISRT
-- 테이블 지정 칼럼 뒤로 추가
ADD COLUMN release_date int(20) NOT NULL AFTER [앞 칼럼명]
```
## 2. 컬럼 삭제 (DROP)
```sql
ALTER TABLE [테이블명] DROP COLUMN [컬럼명];
```
```sql
-- Ex. 
ALTER TABLE testTable DROP COLUMN height;
```

## 3. 컬럼명 변경 (CHANGE)
```sql
ALTER TABLE [테이블명] CHANGE COLUMN [기존컬럼명] [변경할 컬럼명] [컬럼타입];
```
```sql
-- Ex. 
ALTER TABLE testTable CHANGE COLUMN usr_name game_title varchar(50);
```

## 4. 컬럼 타입 변경 (MODIFY)
```sql
ALTER TABLE [테이블명] MODIFY COLUMN [컬럼명] [변경할컬럼타입]
```
```sql
-- Ex.
ALTER TABLE testTable MODIFY COLUMN usr_name varchar(32);
```

# SELECT, INSERT, UPDATE, DELETE
## 1. INSERT 
데이터(레코드)를 삽입하는 명령어 
```sql
INSERT INTO 테이블명[컬럼1, 컬럼2, ...] VALUES[데이터1, 데이터2, ...]
```

```sql
-- Ex. 
mysql> INSERT INTO testTable(id, usr_name, release_date)
    -> VALUES(1, "배틀그라운드", 20171221);
```

## 2. UPDATE
데이터(레코드)를 변경하는 명령어 
```sql
UPDATE 테이블명
SET 수정되어야 할 컬럼명 = 수정되기를 원하는 새로운 값;
[WHERE where_condition]
[ORDER BY ...]
[LIMIT row_count]

--Ex. 
UPDATE testTable
SET date = now()
WHERE id = 1; 
```

## 3. DELETE
데이터(레코드)를 삭제하는 명령어 
```sql
DELETE
FROM 테이블명
WHERE 조건식;
```

## 4. SELECT 
데이터를 조회하는 명령어 
```sql
SELECT 보고 싶은 컬럼명 [AS 별칭]
FROM 테이블명
[WHERE] [조건식]
[ORDER BY]
```
```sql 
-- Ex. 
SELECT * from testTable

SELECT game_title, release_date
FROM testTable
WHERE date IS NOT NULL -- NULL값 보려면 IS NULL 
ORDER BY release_date DESC; 
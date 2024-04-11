# MYSQL 서버의 DBs

```sql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
```

## information_schema
DB의 메타데이터를 보관합니다. MySQL 서버 안의 데이터베이스, 테이블, 칼럼, 타입, 접근권한 등 각 데이터베이스의 정의를 확인할 수 있습니다. 즉, data dictionary와 system catalog에 대한 정보입니다. 

## mysql
시스템 데이터베이스로 mysql 서버가 운영될 때 필요한 정보들을 가지고 있습니다. 구체적으로 권한 관리, 각종 프로그램들(이벤트, 사용자정의기능, 플러그인, 프로시져 등), 로그, 기타 매뉴얼 관련 자료가 포함되어 있습니다.  

## performance_schema
MySQL Server 가 운영중일 때 실행단의 여러 작업들을 모니터링할 때 사용합니다. 쿼리문이 입력되었을 때, 이를 분해, 해석하고 작업하는 일련의 단계들이 잘 진행되는지 (락은 없는지, 싱크로 문제는 없는지 등)를 모니터링합니다. 

## sakila
Sakila 데이터베이스는 MySQL에서 제공하는 샘플데이터입니다. 데이터를 추출, 조작히기에 좋습니다. 

## sys
MySQL 서버의 유저/호스트/세션/쿼리실행 등 MySQL 서버 실행 중의 이력 을 확인할 수 있습니다. DBA 들이 튜닝 또는 진단할 때 유용하게 사용할 수 있습니다. 

##  world
World 데이터베이스는 MySQL에서 제공하는 샘플데이터입니다. 데이터를 추출, 조작하기에 좋습니다. 
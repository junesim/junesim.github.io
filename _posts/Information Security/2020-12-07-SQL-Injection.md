---

title: SQL Injection
categories: [정보보안]

---

SQL Injection에 대해 알아보자.

 <strong>SQL Injection</strong>이란 공격자가 SQL 구문을 이용해 서버의 정보를 탈취하거나 인증을 우회하는 공격 기법이다. 
 
 
 SQL Injection에 많이 사용되는 함수들을 알아보자. 밑에 있는 함수들은 주로 MySQL에서 사용되는 함수들이다.
 
- ## USER
<strong>사용자</strong>와 <strong>호스트</strong>를 출력해주는 함수이다. 함수의 형태는 <strong>user()</strong>이고, select user()로 쿼리를 이용해 현재 사용자와 호스트를 출력할 수 있다. 
 
- ## VERSION
현재 <strong>데이터베이스의 버전</strong>을 출력해주는 함수이다. 함수의 형태는 <strong>version()</strong>이고, select version()로 쿼리를 실행해 현재 데이터베이스의 버전을 확인할 수 있다. 

- ## GROUP_CONCAT
<strong>UNION SELECT</strong>를 이용할 경우 확인할 수 있는 컬럼 수가 제한되는 경우가 많다. 예를 들어 계정 전체를 출력하고 싶은데 출력되는 로우가 하나일 경우 계정 하나 밖에 추출하지 못한다. 이 경우 사용하는 함수가 <strong>group_concat()</strong>이다. SELECT group_concat(name) from users로 쿼리를 돌릴 경우 usres의 name들이 하나의 컬럼으로 합쳐져서 출력된다.
---
title: "CUBRID DB 특정 날짜 주말 OR 주말 제외한 날짜 표시"
categories:
  - CUBRID QUERY
tags:
  - cubrid
  - 주말 제거 or 주말 표시
  - query
  - WEEKEND QUERY
---


Oralce DB 를 사용해왔지만 이번에 취업한 회사는 CUBRID를 사용하기때문 이 또한 공부 해야 한다는 사실
이왕 하는거 즐겁게 하자

ORACLE 에서는 DUAL 이 CUBRID 에서 DB_ROOF 를 사용한다.


# 1. 원하는 날짜 설정하여 상태창에 출력

  - TO_CHAR 로 설정한 날짜 입력
  - TO_DATE 로 설정한 날짜의 문자형태를 'YYYY-MM-DD' 형태의 DATE 로 변환
  - S_DATE : 시작날짜 컬럼명 지정
  - E_DATE : 종료날짜 컬럼면 지정
  - FROM 절에 DB_ROOT 는 오라클 디비에서 사용하던 DUAL 이다.

아래 참조
   ```
   SELECT 
      TO_DATE(TO_CHAR( '2021-01-01'),'yyyy-mm-dd') S_DATE,
      TO_DATE(TO_CHAR('2021-12-31'),'yyyy-mm-dd') E_DATE
   FROM DB_ROOT;
   ```
   

# 2. 원하는 날짜에서 요일은 숫자로, 요일, 날짜 출력
   - LEVEL 를 모르면 계층적 쿼리는 찾아보길 바란다. 모르고 쓰는것보다 알고 쓰는것이 좋다.
   - PL/SQL 를 만들지 안하도 LEVEL로 사용할수 있으니 이 얼마나 좋은가.
   - 아래 쿼리문 참조 바람.
   ```
   SELECT TO_CHAR (S_DATE + LEVEL -1 , 'yyyy-mm-dd') DT ,
		   TO_CHAR(S_DATE + LEVEL - 1 ,'D') D,
		   TO_CHAR(S_DATE + LEVEL -1 ,'DAY') DAILY
		 FROM(
		 				SELECT 
		 							TO_DATE(TO_CHAR( '2021-01-01'),'yyyy-mm-dd') S_DATE,
									TO_DATE(TO_CHAR('2021-12-31'),'yyyy-mm-dd') E_DATE
									FROM DB_ROOT)							
   CONNECT BY LEVEL <= E_DATE - S_DATE +1
   ```


# 3. 주말만 출력 or 주말 제외한 날짜 출력
   - 다시 또 SELECT * FROM 절에 위의 쿼리는 넣어줘야 한다.
   - 그래야 WHERE 절을 쓸수 있더라.
   - 설명하기 귀찮다 그냥 따라 쳐라.

   - 주말만 출력
   ```
      SELECT A.DT, A.D, A.DAILY
      FROM(
            SELECT TO_CHAR (S_DATE + LEVEL -1 , 'yyyy-mm-dd') DT ,
		          TO_CHAR(S_DATE + LEVEL - 1 ,'D') D,
		          TO_CHAR(S_DATE + LEVEL -1 ,'DAY') DAILY
		           FROM(
		 			   	   SELECT 
		 					   		   TO_DATE(TO_CHAR( '2021-01-01'),'yyyy-mm-dd') S_DATE,
							   		   TO_DATE(TO_CHAR('2021-12-31'),'yyyy-mm-dd') E_DATE
							   		   FROM DB_ROOT)							
           CONNECT BY LEVEL <= E_DATE - S_DATE +1) A
      WHERE A.D IN ('1','7');
   ```
    - 주말 제외한 날짜 출력

    ```
      SELECT A.DT, A.D, A.DAILY
      FROM(
            SELECT TO_CHAR (S_DATE + LEVEL -1 , 'yyyy-mm-dd') DT ,
		          TO_CHAR(S_DATE + LEVEL - 1 ,'D') D,
		          TO_CHAR(S_DATE + LEVEL -1 ,'DAY') DAILY
		           FROM(
		 			   	   SELECT 
		 					   		   TO_DATE(TO_CHAR( '2021-01-01'),'yyyy-mm-dd') S_DATE,
							   		   TO_DATE(TO_CHAR('2021-12-31'),'yyyy-mm-dd') E_DATE
							   		   FROM DB_ROOT)							
           CONNECT BY LEVEL <= E_DATE - S_DATE +1) A
      WHERE A.D NOT IN ('1','7');
   ```

  

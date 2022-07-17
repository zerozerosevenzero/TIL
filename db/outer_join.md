-- ■ 예제17. outer join 은 이렇게 튜닝하라 ! 

-- 예제1. 아래의 데이터를 emp 테이블에 입력하고 다음 조인문장의 조인순서를 확인하시오 

insert  into  emp(empno, ename, sal, deptno )
values( 2921, 'JACK', 4500, 70 );

select  /*+ gather_plan_statistics */  e.ename, d.loc
from   emp  e,  dept  d
where   e.deptno = d.deptno (+);

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 예제2. 다음 SQL의 조인순서를 dept ---> emp 순이 되게하시오 !

select  /*+ gather_plan_statistics */  e.ename, d.loc
from   emp  e,  dept  d
where   e.deptno = d.deptno (+);

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

select  /*+ gather_plan_statistics leading(d e) use_hash(e) */  e.ename, d.loc
from   emp  e,  dept  d
where   e.deptno = d.deptno (+);

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- swap_join_inputs 를 쓰면 ?

select  /*+ gather_plan_statistics leading(d e) use_hash(e) swap_join_inputs(d) */  e.ename, d.loc
from   emp  e,  dept  d
where   e.deptno = d.deptno (+);

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 메모리 사요량이 줄어들었음

-- 문제. 아래의 SQL을 튜닝하시오

create table products100
as
 select * from sh.products;
 
select /*+ gather_plan_statistics leading(s c) use_hash(c) */ s.*
  from  sales100 s , customers100  c
   where s.cust_id(+) = c.cust_id and s.time_id='98/01/10';

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

--  4567

--답:

select /*+ gather_plan_statistics leading(c s) use_hash(s) swap_join_inputs(c) */ s.*
  from  sales100 s , customers100  c
   where s.cust_id(+) = c.cust_id and s.time_id='98/01/10';

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 1527

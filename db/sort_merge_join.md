# sort merge join

Non equal join 일 경우 보통 사용
정렬을 조인하면서함 

-- ■ 예제16. 이럴때는 sort merge join 으로 유도하라 !

-- 예제1. 아래의 조인문을 해쉬조인으로 유도하시오 !

-- 조인순서: salgrade ---> emp
-- 조인방법:  해쉬조인 

 select  /*+ gather_plan_statistics  */
       e.ename,  e.sal,  s.grade
  from  emp  e, salgrade  s
  where e.sal  between  s.losal   and  s.hisal; 

-- 해쉬조인으로 유도하면?

 select  /*+ gather_plan_statistics  leading(s  e)  use_hash(e) */
       e.ename,  e.sal,  s.grade
  from  emp  e, salgrade  s
  where e.sal  between  s.losal   and  s.hisal; 

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 소트머지 조인으로 유도하면?

 select  /*+ gather_plan_statistics  leading(s  e)  use_merge(e) */
       e.ename,  e.sal,  s.grade
  from  emp  e, salgrade  s
  where e.sal  between  s.losal   and  s.hisal; 

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 예제2. sort merge join 은 정렬된 결과를 출력한다. 

select /*+ gather_plan_statistics  leading(d  e) use_hash(e) */ e.ename, d.loc, e.deptno
 from  emp  e, dept  d
  where  e.deptno= d.deptno
  order by e.deptno asc;

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 버퍼의 갯수:13개

select /*+ gather_plan_statistics  leading(d  e) use_merge(e) */ e.ename, d.loc, e.deptno
 from  emp  e, dept  d
  where  e.deptno= d.deptno;

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 버퍼의 갯수:12개

-- 문제. 아래의 SQL을 sort merge join 으로 유도하시오

select /*+ gather_plan_statistics leading(n c s) use_hash(c) use_hash(s)   */ 
  c.cust_id,  sum(s.amount_sold)
  from   sales100  s, customers100  c, countries100  n
  where   s.cust_id = c. cust_id
  and  c.country_id = n. country_id
  and n.country_name='France'
  group by c.cust_id
  order by c.cust_id asc;
  
SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

--5964

--- sort merge 조인으로 유도후:

select /*+ gather_plan_statistics leading(n c s) use_merge(c) use_merge(s)  */ 
  c.cust_id,  sum(s.amount_sold)
  from   sales100  s, customers100  c, countries100  n
  where   s.cust_id = c. cust_id
  and  c.country_id = n. country_id
  and n.country_name='France'
  group by c.cust_id;
  
SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 5962




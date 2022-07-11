# 1. nested loop 조인과 hash 조인 비교 

## nested loop 조인으로 수행했을때 

select  /*+ gather_plan_statistics  leading(d e) use_nl(e) */  e.ename,  d.loc  
from  emp  e, dept  d  
where  e.deptno = d.deptno;  

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 버퍼의 갯수 : 30개

* * *
## 해쉬조인으로 수행했을때

select  /*+ gather_plan_statistics  leading(d e) use_hash(e) */  e.ename,  d.loc  
from  emp  e, dept  d  
where  e.deptno = d.deptno;  

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));  

-- 버퍼의 갯수 : 13개
 * * *
 
 # 2. 검색 조건이 있었을때의 해쉬조인

## 조인 순서가 emp --> dept 순일때

select /*+ gather_plan_statistics  leading(e d) use_hash(d) */  e.ename, d.loc                         
  from  emp  e, dept  d
  where  e.deptno = d.deptno  
    and  e.job='SALESMAN'
    and  d.loc='CHICAGO'; 

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 버퍼의 갯수:  10887

## 조인 순서가 dept ---> emp 일때 

select /*+ gather_plan_statistics  leading(d e) use_hash(e) */  e.ename, d.loc                         
  from  emp  e, dept  d
  where  e.deptno = d.deptno  
    and  e.job='SALESMAN' 
    and  d.loc='CHICAGO';   

SELECT * FROM TABLE(dbms_xplan.display_cursor(null,null,'ALLSTATS LAST'));

-- 버퍼의 갯수: 13개 



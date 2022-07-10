#  nested_loop_join
조인의 순서를 조정하는 힌트 
아래 쿼리에서 보면 e -> d
select /*+ gather_plan_statistics leading(e d) use_nl(d) */ e.ename, d.loc  
from emp e, dept d   
where e.deptno = d.deptno;.  

보통은 데이터의 크기가 작은테이블에서 큰테이블로 조인 
조건이 있는 경우 조건이있는 테이블 먼저 조인

※ 조인 순서를 결정하는 힌트 2가지 ?  
1. ordered : from 절에서 기술한 테이블 순서데로 조인해라 ~
2. leading :  leading 힌트 안에 사용한 테이블 순서데로 조인해라~

select /*+ gather_plan_statistics  ordered use_nl(d) */  e.ename,  e.sal,  d.loc  
   from  emp  e,  dept  d  
   where  e.deptno = d.deptno;  

select /*+ gather_plan_statistics  leading(e d) use_nl(d) */  e.ename,  e.sal,  d.loc   
   from  dept  d, emp  e  
   where  e.deptno = d.deptno;  
   
* * *


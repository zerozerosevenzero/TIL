#  nested_loop_join
조인의 순서를 조정하는 힌트 
아래 쿼리에서 보면 e -> d
select /*+ gather_plan_statistics leading(e d) use_nl(d) */ e.ename, d.loc  
from emp e, dept d   
where e.deptno = d.deptno;.  

보통은 데이터의 크기가 작은거에서 큰거로 조인 
조건이 있는 경우 조건이있는 테이블 먼저 조인

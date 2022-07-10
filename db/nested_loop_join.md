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

1. 인덱스 없었을때의 2개의 테이블 조인

select /*+ gather_plan_statistics leading(e d) use_nl(d) */  e.ename,  e.sal,  d.loc  
from  emp  e,  dept  d  
where  e.deptno = d.deptno;  
결과: buffer 35개
* * *
2. 연결고리가 되는 컬럼에 인덱스 생성후 결과 

create index emp_deptno on emp(deptno);  

select /*+ gather_plan_statistics leading(d e) use_nl(e) */  e.ename,  e.sal,  d.loc  
from  emp  e,  dept  d  
where  e.deptno = d.deptno;  
결과: buffer 10개 
* * *
3. 검색 조건이 있었을때의 두개의 테이블 조인 

select /*+ gather_plan_statistics leading(e d) use_nl(d) */  e.ename,  e.sal,  d.loc  
from  emp  e,  dept  d   
where  e.deptno = d.deptno and e.ename='SCOTT';  
결과: buffer 14개
* * *
4. 연결고리가 되는 컬럼에 인덱스를 생성한 후에 조인

create index dept_deptno on dept(deptno);  

select /*+ gather_plan_statistics leading(e d) use_nl(d) */  e.ename,  e.sal,  d.loc  
from  emp  e,  dept  d  
where  e.deptno = d.deptno and e.ename='SCOTT';  
결과: buffer 9개
* * *
5. ename 에 인덱스를 생성했을때  
create index emp_ename on emp(ename);  
select /*+ gather_plan_statistics leading(e d) use_nl(d) */  e.ename,  e.sal,  d.loc  
from  emp  e,  dept  d   
where  e.deptno = d.deptno and e.ename='SCOTT';  
결과: buffer 4개
* * *
6. 검색조건이 여러개 있었을때의 조인 (인덱스 없었을때)  
select /*+ gather_plan_statistics leading(d e) use_nl(e) */ e.ename, e.sal, d.loc  
from  emp  e,  dept  d  
where  e.deptno = d.deptno  and e.job='SALESMAN'  
and d.loc='CHICAGO';  
결과: buffer 14개  
* * *
7. 연결고리가 되는 컬럼에 인덱스가 있었을때   
create index emp_deptno on emp(deptno);

select /*+ gather_plan_statistics leading(d e) use_nl(e) */ e.ename, e.sal, d.loc  
from  emp  e,  dept  d  
where  e.deptno = d.deptno  and e.job='SALESMAN'  
and d.loc='CHICAGO';  

결과: buffer 9개  
* * *
8. 부서위치에도 인덱스를 생성했을때 

create index dept_loc on dept(loc);  

select /*+ gather_plan_statistics leading(d e) use_nl(e) */ e.ename, e.sal, d.loc  
from  emp  e,  dept  d  
where  e.deptno = d.deptno  and e.job='SALESMAN'  
and d.loc='CHICAGO';  
결과:  buffer 4개 

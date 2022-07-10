# index range scan descending
1. 과도한 데이터 정렬 작업은 데이터베이스에 부하를 준다
2. 정렬작업을 수행하는 데이터 베이스의 메모리 공간은 한정되어 있다.
3. 정렬작업을 피하기 위해서는 이미 정렬이 되어져있는 인덱스를 활용하는 방법이 있습니다.
4. 정렬된 결과를 볼 필요가 없다면 굳이 정렬을 일으키는 SQL을 작성하지 않는 것이 바람직하다.

* * *

create index emp_sal on emp(sal);

select /* + gather_plan_statistics index_desc(emp emp_sal) */ ename, sal  
from emp  
where sal >=0;   // where절을 꼭 써줘야 인덱스 발동
* * *
<img width="698" alt="image" src="https://user-images.githubusercontent.com/46700734/178135955-a7a7277d-a4b8-41c2-97f4-799d0b1b0f5e.png">
* * *


# max 값 가져오기

튜닝전: -> sort aggregate 가 실행됨  

select /* + gather_plan_statistics index_desc(emp emp_sal) */ max(sal). 
from emp

튜닝후:

select /* + gather_plan_statistics index_desc(emp emp_sal) */ max(sal). 
from emp
where sal >= 0 and rownum =1;  //rownum이 1인건만

* * *


create  index  emp_deptno_sal  on  emp(deptno, sal) ;

튜닝전:   
select /*+ gather_plan_statistics */  empno, deptno, sal
                  from  emp
                  where  deptno = 20
                  order  by  sal  desc; 


튜닝후: 소트없이 결과가 인덱스기반으로 출려됨
 
select /*+ gather_plan_statistics  index_desc(emp  emp_deptno_sal) */ 
                 empno, deptno, sal
   from  emp
  where  deptno = 20;


* * *

튜닝전:

select /*+ gather_plan_statistics */ ename, hiredate
              from  emp
              where  to_char(hiredate, 'RRRR') ='1981'
              order by  hiredate  desc; 



튜닝후: 소트없이 결과가 인덱스기반으로 출려됨

create  index  emp_hiredate  on  emp(hiredate); 

select /*+ gather_plan_statistics  index_desc(emp emp_hiredate) */ 
      ename, hiredate
       from  emp
       where  hiredate  between   to_date('1981/01/01', 'RRRR/MM/DD')
                                    and   to_date('1981/12/31', 'RRRR/MM/DD');
* * *

--- 튜닝전:  
select   /*+ gather_plan_statistics */  ename, job, sal
            from  emp
            where  substr(job, 1, 5 )='SALES'
            order by  sal  desc;

select * from table(dbms_xplan.display_cursor(null, null, 'ALLSTATS LAST'));

--- 튜닝후:  
create  index emp_job_sal   on  emp(job, sal);

 select   /*+ gather_plan_statistics  index_desc(emp emp_job_sal) */  
             ename, job, sal
   from  emp
   where  job  like  'SALES%' ;

select * from table(dbms_xplan.display_cursor(null, null, 'ALLSTATS LAST'));


# index range scan descengind

create index emp_sal on emp(sal);

select /* + gather_plan_statistics index_desc(emp emp_sal) */ ename, sal  
from emp  
where sal >=0;   // where절을 꼭 써줘야 인덱스 발동


<img width="698" alt="image" src="https://user-images.githubusercontent.com/46700734/178135955-a7a7277d-a4b8-41c2-97f4-799d0b1b0f5e.png">

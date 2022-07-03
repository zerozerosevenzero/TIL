index full scan vs index fast full scan
Fast full scan 은 보통 group by 와 많이 쓰임
<img width="832" alt="image" src="https://user-images.githubusercontent.com/46700734/177025659-8603e865-9da4-4864-9e03-aae12d5d27bb.png">

<img width="1015" alt="image" src="https://user-images.githubusercontent.com/46700734/177024600-c510b9e5-fa2c-4615-87bb-cec4febd1881.png">

index fast full scan을 할 때는 인덱스에걸리는 컬럼이 not null 제약이 걸려있어야함
또는
where 절에 null이 아님을 명시해주어야 index full scan을 피하고 index fast full scan을 실행시킬 수 있음
(ex)
<img width="1180" alt="image" src="https://user-images.githubusercontent.com/46700734/177025501-ae7e6174-97b8-48b1-9257-b8a21b7949fc.png">


<img width="1014" alt="image" src="https://user-images.githubusercontent.com/46700734/177025768-183368cd-aae4-4b45-b121-cefc391632de.png">

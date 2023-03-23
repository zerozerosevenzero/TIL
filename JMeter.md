# JMeter
성능 측정 및 부하 (load) 테스트 기능을 제공하는 오픈 소스 자바 애플리케이션.

## 주요개념
- Thread Group: 한 쓰레드 당 유저 한명
- Sampler: 어떤 유저가 해야 하는 액션
- Listener: 응답을 받았을 할 일 (리포팅, 검증, 그래프 그리기 등)
- Configuration: Sampler 또는 Listener가 사용할 설정 값 (쿠키, JDBC 커넥션 등)
- Assertion: 응답이 성공적인지 확인하는 방법 (응답 코드, 본문 내용 등)



## JMeter m1에서 실행하기 
```
open /opt/homebrew/bin/Jmeter
```

<img width="1537" alt="image" src="https://user-images.githubusercontent.com/46700734/227241368-3129cda7-f25b-4257-962a-6b39c17b71b1.png">


---

1-1. 쓰레드 그룹 만들기
<img width="1529" alt="image" src="https://user-images.githubusercontent.com/46700734/227243212-72356b5e-9451-4d01-b9ad-efdf5952abae.png">

1-2. Number of Threads와 Ramp-up Period 정의하기
그림예시: 10초안에 5명의 쓰레드를 만들어라
<img width="1154" alt="image" src="https://user-images.githubusercontent.com/46700734/227243439-f5d49c7c-16b6-4346-9c10-6d0def5c5917.png">

1-2. Loop count: 몇번을 반복 시킬건지

1-2. 장애발생 시 어떤 동작을 취할지 선택
<img width="1170" alt="image" src="https://user-images.githubusercontent.com/46700734/227244134-ccef6aea-00fa-42ac-98a1-cf26b4c5c674.png">


---
# Sampler 
유저들이 어떤행동을 하지 행동을 정의

2-1. HTTP request에 대한 Sampler 만들기
<img width="1024" alt="image" src="https://user-images.githubusercontent.com/46700734/227244969-9b7ce30c-9ca6-4bfc-a2fc-e1562e2115fd.png">

---
# Listner
<img width="893" alt="image" src="https://user-images.githubusercontent.com/46700734/227250877-cb3841cd-aeec-478d-a792-4e4393835abe.png">








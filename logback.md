# LogBack

### Appender 
- ConsoleAppender: 콘솔에 log를 출력
- FileAppender: 파일 단위로 log를 저장
- RollingFileAppender: 설정옵션에 따라 log를 여러 파일로 나누어저장
- SMTPAppender: log를 메일로 전송 하여 기록
- DBAppender: log를 db로 저장

## logback-spring.xml
기본 스프링부트 로그설정
<img width="697" alt="image" src="https://user-images.githubusercontent.com/46700734/213848029-2740d980-528f-4caa-b640-3e12b84cb738.png">

해당 설정을 통해 스프링부트의 기본 로그 설정을 참조할 수 있음
logback 프로필 설정을 통해 각 프로필별 설정 구성 가능

logback-spring-local.xml
<img width="858" alt="image" src="https://user-images.githubusercontent.com/46700734/213848788-569f2766-90a5-492e-a8ca-ae90e274645c.png">
- appender를 통해 CONSOLE2 appender 추가
- 해당 appender는 ConsoleAppender
- 기존 CONSOLE appender는 console-appender.xml에 정의
- appender의 filter > level에 debug 레벨 정의 가능
- appender의 pattern을 통해 로그 메시지 정의 가능

--- 
## RollingFileAppender 사용하기
<img width="744" alt="image" src="https://user-images.githubusercontent.com/46700734/213849355-f19eafe3-b3d6-4753-979b-65b3f3c79635.png">

- <file> 어떤 파일에 해당 로그를 쌓을 건지를 정의 (logs폴더의 request1.log)
- <rollingPolicy> 파일이 어떤식으로 저장할지 정의
- fileNamePattern 파일 이름을 어떤식으로 저장할지
- maxFileSize 로그파일 최대 크기
- maxHistory 로그파일 최대 보관주기 단위 (일)
- outputPatternAsHeader: 로그가 어떤 패턴으로 쌓이는지 첫줄에 보여줌  
  ![image](https://user-images.githubusercontent.com/46700734/213872550-e9dcdcad-12d4-46c5-b2f8-d04a90faeadf.png)

---
## LogBack 변수만들기
![image](https://user-images.githubusercontent.com/46700734/213872717-d41aeeab-9407-4df7-8c52-18d21104b534.png)

  
  

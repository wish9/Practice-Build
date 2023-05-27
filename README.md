[빌드/실행/배포 블로그 포스팅 주소](https://velog.io/@wish17/%EC%BD%94%EB%93%9C%EC%8A%A4%ED%85%8C%EC%9D%B4%EC%B8%A0-%EB%B0%B1%EC%97%94%EB%93%9C-%EB%B6%80%ED%8A%B8%EC%BA%A0%ED%94%84-59%EC%9D%BC%EC%B0%A8-Spring-MVC-%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EB%B9%8C%EB%93%9C%EC%8B%A4%ED%96%89%EB%B0%B0%ED%8F%AC)

# Spring 애플리케이션 빌드/실행/배포

[연습내용 GitHub주소](https://github.com/wish9/Practice-Build/commit/5ce7324ff744a00fec79b3a213ec616961203752) resource만 보면 됨.

 IntelliJ IDE에서는 아래와 같이 Gradle task 명령을 통해 빌드 할 수 있다.
 
 ![](https://velog.velcdn.com/images/wish17/post/b620227e-83a7-4b33-8cea-e9b7b9f6ccb4/image.png)

``:build``
- ``:assemble``, ``:check`` 같이 Gradle에서 빌드와 관련된 모든 task들을 실행
- 실행 가능한 Jar 파일 이외에 plain Jar 파일 하나를 더 생성

``:bootJar``
- 빌드와 관련된 모든 task들을 실행하는 것이 아니라 애플리케이션의 실행 가능한 Jar(Executable Jar)파일을 생성하기 위한 task만 실행
- Executable Jar 파일**'만'** 필요하면 사용하면 됨

###  IntelliJ IDE를 사용하지 않고 빌드하는 방법

cmd, Git Bash, Windows Power Shell, 터미널 등 콘솔에 Gradle task 명령어를 입력하면 된다.

1. 프로젝트가 위치해 있는 디렉토리 경로로 이동

2. Gradle task를 CLI 명령으로 입력할 수 있는 콘솔창을 템플릿 프로젝트 root 경로에서 오픈

3. 명령어 입력
- Windows 터미널
    - ``PS D:\codestates\project\section3-week4-build> .\gradlew bootJar``

- Git Bash
    - ``MINGW64 /d/codestates/project/kdt/for-ese/section3-week4-build (main)``
    - ``$ ./gradlew build``
    
![](https://velog.velcdn.com/images/wish17/post/1f4d0403-ffef-42aa-afd0-adbf86bd7b08/image.png)
    

### 애플리케이션 실행

1. 빌드를 통해 생성된 Jar 파일이 있는 디렉토리 경로로 이동

![](https://velog.velcdn.com/images/wish17/post/c50e5265-8558-4b30-a360-ead1abb0815b/image.png)


2. 콘솔 오픈 후 ``java -jar 파일명.jar`` 입력

![](https://velog.velcdn.com/images/wish17/post/1ad5eccf-4073-448c-a156-5b41f96d6137/image.png)

###  프로파일(Profile) 적용

> 프로파일 기능은 빌드된 실행 파일을 어느 환경에서 실행할 지 여부를 결정할 때 주로 사용


``application.yml``
- 일반적으로 애플리케이션 실행 환경에 상관없는 공통 정보들은 application.yml에 설정

``application-local.yml``
- 로컬 환경에서 사용하는 정보들은 application-local.yml 파일에 설정

``application-server.yml``
- 서버 환경에서 사용하는 정보들은 application-server.yml 파일에 설정



###  IntelliJ IDE에서 프로파일 적용

구성편집

![](https://velog.velcdn.com/images/wish17/post/ad1de26e-cbcf-4291-9f34-97026c7a27c1/image.png)

프로그램 인수 ``--spring.profiles.active=local``와 같이 local로 변경

![](https://velog.velcdn.com/images/wish17/post/7812621b-3b7d-40c0-aa9d-134298670ea2/image.png)

###  빌드된 실행 파일에 프로파일 적용

위에서 사용했던 ``java -jar 파일명.jar``에 ``--spring.profiles.active=local``을 추가하면 된다.

```
//예시
PS D:\AAWonJong\it\spring\project\be-template-build\build\libs> java -jar section3-week3-template-build-0.0.1-SNAPSHOT.jar --spring.profiles.active=local
```

![](https://velog.velcdn.com/images/wish17/post/244c676f-07b4-4b58-b305-076f7cf0c52b/image.png)

### 간단하게 알아보는 배포 방법

- 전통적인 배포 방법
    - scp나 sftp 같은 표준 유닉스 툴을 이용해서 서버로 전송
    - 서버로 전송된 Jar 파일은 JVM이 설치된 환경이라면 어디서든 실행 가능

-  클라우드 서비스를 이용한 배포 방법
    - PaaS(Platform as a Service)
		- 애플리케이션을 개발하고 실행하기 위한 플랫폼을 제공한다.
		- 플랫폼이 서버, 스토리지, 네트워크 및 데이터베이스와 같은 인프라를 관리해 줌.
		- 예시: Heroku, Google App Engine, Microsoft Azure 등이 있다.

    - IaaS(Infrastructure as a Service)
		- 개발자가 직접 인프라를 관리할 수 있는 플랫폼을 제공한다.
		- 서버, 스토리지, 네트워크 및 데이터베이스와 같은 인프라를 개발자가 직접 관리한다.
		- 예시: Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform 등이 있다.

    - CI/CD 플랫폼을 사용한 배포
		- 지속적인 통합 및 배포를 제공하는 플랫폼이다.
		- 코드를 버전 관리 시스템에 커밋하면 자동으로 빌드, 테스트, 배포되도록 설정할 수 있다.
		- 대표적인 예시: Jenkins, CircleCI, Travis CI, GitLab CI/CD 등이 있다.

***

## Spring Boot 애플리케이션 Build 및 실행 실습

### MySQL 사용법

워크벤치에 [스키마 추가](https://coderzero.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-MySQL-Workbench)

![](https://velog.velcdn.com/images/wish17/post/fe943b0e-d195-4dfb-a677-df51c8d0c49f/image.png)

![](https://velog.velcdn.com/images/wish17/post/856079aa-a160-4bcf-825d-f96e2cdb49c6/image.png)


혹은 command line 사용해서 원하는 디비 생성, 접속하고 원하는 요청을 쿼리문으로 날려주면 된다.

![](https://velog.velcdn.com/images/wish17/post/447e7e28-95eb-42c4-b299-57f34b70e248/image.png)



### 인텔리제이 빌드, yml

- ``application-server.yml`` 파일 설정

```yml
# 서버 환경에서 사용하는 정보들은 application-server.yml 파일에 설정
# TODO MySQL DB 접속 정보를 아래에 설정하세요
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/orderCoffee?serverTimezone=Asia/Seoul # url설정
    username: root
    password: 비밀번호입력!
    Driver-class-name: com.mysql.cj.jdbc.Driver # 드라이버 설정
  jpa:
    hibernate:
      ddl-auto: create  # 스키마 자동 생성
    show-sql: true      # SQL 쿼리 출력
    properties:
      hibernate:
        format_sql: true  # SQL pretty print
```

![](https://velog.velcdn.com/images/wish17/post/81dff8ba-4f52-4f62-8c53-6cfb52405be8/image.png)


- ``build.gladle`` 설정
    - ``runtimeOnly 'mysql:mysql-connector-java:8.0.32'`` 의존성 추가

![](https://velog.velcdn.com/images/wish17/post/b9ebdd85-8287-4dd6-a404-e0c58c865709/image.png)

- 빌드

![](https://velog.velcdn.com/images/wish17/post/b8a8d553-bb2f-46fe-b510-c10aba4e6afc/image.png)


- 빌드 후 구성편집

![](https://velog.velcdn.com/images/wish17/post/98427891-d99f-453e-bb37-d6144b7a227b/image.png)

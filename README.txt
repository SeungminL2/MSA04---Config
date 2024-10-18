*** Git에 repository 만들어야함
	|-> (참고) https://dukcode.github.io/spring/spring-cloud-config/ 
	|		|-> 일단은 private이 아닌 public으로 만들었음
	|-> (참고) https://wonit.tistory.com/502

[ ConfigServer ]
	|-> Dependency
	|	|-> Spring Boot DevTools
	|	|-> Spring Web
	|	|-> Eureka Discovery Client
	|	|-> Config Server
	|	|-> actuator
	|
	|-> ConfigServerApplication.java
	|	|-> @EnableConfigServer
	|
	|-> application.yml
		|-> 포트번호 8888
		|-> config 추가

[ Service01, Service02 ]
	|-> Dependency
	|	|-> Config Client
	|	|	|-> Service02에서는 우클릭 >> Spring >> add starters에서 클릭
	|	|	|-> Service01에는 복사붙여넣기?
	|	|-> Cloud Bootstrap
	|		|-> 추가 후에 맨 뒤에 -bootstrap 붙여야함
	|		|-> <artifactId>spring-cloud-starter-bootstrap</artifactId>
	|
	|-> !! Git !!
	|	|-> 전체 서비스에 공통적으로 적용되는 코드 저장
	|	|	|-> application.yml 생성
	|	|		|-> eureka관련 코드
	|	|-> 만약 service01에 적용되는 코드가 있다면?
	|		|-> application-service01.yml 생성
	|
	|-> bootstrap.yml 파일 생성
		|-> 애플리케이션이 시작되자마자 바로 적용되야하는 설정들
		|	|-> bootstrap.yml이  Git에 저장된 application.yml보다 먼저 실행됨
		|-> src/main/resource에 위치함
			|-> spring.application.name
			|-> 포트번호 지정
			|-> spring.cloud.config 추가
			|-> resilience4j 관련 코드

*** Git에 저장된 application.yml파일 보기
	|-> http://localhost:8888/config-test/service01
	|-> http://localhost:8888/config-test/service02
		|-> "propertySources": [ ] 안에 application.yml 내용 들어있어야함
	

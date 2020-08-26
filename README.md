## 파스타 클라우드에 mysql용 스프링프로젝트 배포하기

***
### 파스타 클라우드 활용(공통)
1. 스프링프로젝트 khj_mysql 변경 (도메인의 호스트네임으로 사용)
2. 이클립스에서 khj_mysql 프로젝트를 파스타에 배포
3. khj_mysql 로컬 mysql서버와 연동처리
4. 파스타 클라우드에서 Mysql서비스 생성(원격접속이름과 암호를 확인가능)
5. 원격 phpmyadmin 툴(워크벤치와 비슷)을 파스타 클라우드 PHP앱 생성 후 배포
6. khj_mysql 프로젝트를 클라우드용 DB사용으로 변경 후 파스타에 재배포
	http://khj_mysql.paas-ta.org
7. egov_sht 프로젝트 이름 변경 : egov_khj 파스타에 배포(Mysql클라우드 사용)
	http://khj_egov.paas-ta.org
***

### 20200812(수) 작업내용
- 4. 스프링mysql프로젝트를 로컬Mysql로 설정 -> 클라우드 파스타용으로 변경

```
- 3) 작업결과 확인: 이클립스에서 파스타서버 더블클릭 -> Application and Service 탭에서 -> 오른쪽에 update and Restart 버튼은 클릭해서 클라우드 배포에 수정사항 적용
- 2) root-context.xml 파일에 DB커넥션 설정을 클라우드용으로 추가
- 1) maven -> pom.xml 파일에 클라우드 모듈 추가
```

- 3. 로컬에서 테스트 완료 후 Mysql 서비스를 생성 

```
- 4) http://khj-myadmin.paas-ta.org 접속 후 edu DB생성 및 더미 데이터 입력
- 3) 아래 php 프로젝트를 파스타에 push (이때 manifest.yml 사용) : 클라우드파운더리 --- cf CLI 설치(command line interface) <-> GUI
- 2) 생성된 Mysql 서비스를 웹으로 제어하는 php 프로젝트를 이클립스로 임포트 (khj-myadmin 프로젝트명)
- 1) 온라인 파스타 클라우드에서 khj-mysql-db 이름의 Mysql 서비스 생성 
```

- 2.kjh-mysql 프로젝트를 Hsql -> Mysql로 변경

```
- 2) wamp 실행 후 프로젝트를 톰캣서버로 확인
- 1) root-context.xml 수정
```

- 1.어제한 내용 리뷰
- 파스타클라우드에 접속할 때 https://api.paas-ta.org 주소사용
- RestAPI 서버 = https://api.paas-ta.org
- RestAPI서버에 Json데이터를 보내서 앱을 생성 + 실행하게 됨

```
매니페스트 야믈 파일(manifest.yml)
키 : 값
---
applications:
- name: khj-mysql
  memory: 1024M
  disk_quota: 1024M
  instances: 1
  host: khj-mysql
  domain: paas-ta.org
```
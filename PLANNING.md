# 🎓mojolll(모두의졸전) 백엔드 개발 계획

## Menu Structure
![메뉴 구조(사이트맵)](https://user-images.githubusercontent.com/110734817/223634922-7e4ed6c2-5fe5-40a8-bb8a-841ff7d71696.png)

## ERD
<img width="581" alt="ERD-mojolll" src="https://user-images.githubusercontent.com/110734817/224912908-25b233f5-1b9c-4c13-aec0-affb1c7680b7.png">


## CRUD
|대구분|중구분|사용자|Create(쓰기)|Read(읽기)|Update(수정)|Delete(삭제)|비고|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|전시|개인 졸업전시 작성|일반 회원|X|O|X|X|학교이메일 인증을 안한 회원|
|||학교인증 회원|O|O|O|O|1개의 글만 쓸 수 있다. (임시저장 기능 몇 초마다 할 것인지)|
||이미지 등록|일반회원|X|X|X|X|학교이메일 인증을 안한 회원|
|||학교인증 회원|O|O|O|O|이미지 크기 한계 설정, 이미지 공유기능, 이미지 최적화를 어떻게 할 것인지(썸네일 이미지를 따로 추출한다. 혹은 다른 의견)|

## API
|URL|HTTP Method|상태|Comment|
|:---:|:---:|:---:|:---:|
|v1/auth/signup|POST||회원가입|
|v1/auth/login|POST||로그인 (토큰O)|
|v1/auth/login/kakao|GET||카카오 로그인 (토큰X)|
|v1/auth/login/naver|GET||네이버 로그인 (토큰X)|
|v1/users|GET||회원 정보 조회|
|v1/users|PUT||회원 정보 수정|
|v1/users/user|DELETE||회원탈퇴|
|v1/boards/category|GET||카테고리로 게시물 조회|
|v1/boards/university|GET||대학교로 게시물 조회|
|v1/boards/user|GET||유저로 게시물 조회|

---

개발과 동시에 테스트 코드를 작성하려고 합니다. (설계 -> 테스트 (->설계 수정) -> 개발)

- Junit을 이용한 Unit Test(단위 테스트)
- Mockito mock을 이용한 단위 테스트

3월

- CRUD, E-R Diagram 작성 및 API 명세서 작성
  - **_ER diagram (Entity-Relationship Model)_**
    현실세계의 요구사항(Requirements)들로 부터 Database를 설계과정

4월

- JWT 로그인 로그아웃 구현
  - JWT
    JSON 웹 토큰은 선택적 서명 및 선택적 암호화를 사용하여 데이터를 만들기 위한 인터넷 표준으로 JWT 토큰 탈취 이슈 처리
    - Redis 및 Elasticsearch 적용
    - *Access Token* & Refresh Token 방식
  - 정규 표현식 및 DB를 이용한 로그인 보안 이슈 처리하기
  - 대학교 email 인증
  - MySQL DB설계

5월

- OAuth 2.0 기반 SSO 동작 구현 및 Spring Security 적용 및 CORS 처리
  - **_Single Sign_**-**On**(**_SSO_**)
    1회 사용자 인증으로 다수의 애플리케이션 및 웹사이트에 대한 사용자 로그인을 허용하는 인증 솔루션입니다. (Naver, Kakao 로그인 구현)

6월

- REST API 개발 및 이미지 저장을 위한 AWS S3기능 적용
  - 각 대학교에서 졸업전시 권한을 가진 인원만 처리하도록 JWT + RBAC(Role Based Access Control)기반 \*\*Spring Security 적용

7월

- Parmater 변조, SQL INJECTION, CSRF(Cross-site request forgery)등 보안 이슈 처리하기
- spring boot 프로메테우스 모니터링 시스템 구축

8월

- 도메인 구매
- AWS Iaas(Infrastructure as a Service) EC2 배포
- CI(오픈소스 Travis CI 사용), CD(AWS CodeDeploy) 환경 구축
  - 코드 버전 관리를 하는 VCS시스템(Git, SVN등)에 PUSH가 되면 자동으로 테스트와 빌드가 수행되어 안정적인 배포 파일을 만드는 과정을 CI(Continuous Integration - 지속적 통함) 이라고 한다. 이 빌드 결과를 자동으로 운영 서버에 무중단 배포까지 진행되는 과정을 CD(Continuous Deployment -지속적인 배포) 라고 한다.
    
- AWS S3를 이용해서 CodeDeploy가 Travis CI가 빌드한 결과를 가져갈 수 있도록 보관한다.
- 엔진엑스(Nginx)를 이용한 무중단 배포 환경 구축
  - 웹 서버, 리버스 프록시, 캐싱, 로드 밸런싱, 미디어 스트리밍 등을 위한 오픈소스 소프트웨어로 여러기능 외부의 요청을 받아 백엔드 서버로 요청을 전달하는 리버스 프록시 기능을 사용하여 무중단 배포 환경      구축한다.
  - 리버스 프록시 서버(엔진엑스)는 요청을 전달하고 실제 요청에 대한 처리는 뒷단의 웹 애플리케이션 서버들이 처리한다.
혹은 AWS에서 블루 그린(Blue-Green) 무중단 배포 , 도커를 이용한 웹서비스 무중단 배포

9월
- 실제 사용자 서비스 제공

# 🔫 2022-TEAM.Harmony 기여사항 및 프로젝트 트러블 슈팅

### ⛑ 내가 기여한 점

#### 1. 뉴스 데이터 수집 (크롤링, naver summary api)
> - python selenium을 이용한 네이버 스포츠 뉴스 Top100 크롤링
> - 네이버 summary api를 이용한 뉴스 본문 내용 요약

#### 2. 뉴스 도메인 기능 구현, 북마크 도메인 기능 구현 (CRUD)
> - 요청에 따른 뉴스 정보 리스팅, 조회수 기능 구현
> - 북마크 생성, 삭제, 조회 구현

#### 4. XSS 공격 방어 (using WebMvcConfigure)
> - [`WebMvcConfigure`](https://blog.naver.com/cksgurwkd12)를 상속받아 [`MappingJackson2HttpMessageConverter`](https://blog.naver.com/cksgurwkd12)를 재정의해 방어했다.* 

#### 5. 배포 후 모니터링 목적의 전역 예외처리와 로그백 (advice, slf4j)
> - AOP와 Advice, sl4j이용
> - [전역 예외처리에 Advice를 적용한 이유](https://blog.naver.com/cksgurwkd12)

#### 6. AWS EB 환경 구축 및 git action (based on spring)를 이용한 CI/CD 구축
> - [ROUTE53을 이용한 SSL 생성 및 CertificationManager에 등록](https://blog.naver.com/cksgurwkd12/222845288814)
> - [EB와 CloudFront 생성과 SSL 인증서 적용](https://blog.naver.com/cksgurwkd12/222845310032)
> - [git cation을 이용한 CI/CD 구축](https://blog.naver.com/cksgurwkd12/222845312289)
([Front](https://github.com/2022-Harmony/NewsCommunity-bFinal/actions), [Backend](https://github.com/2022-Harmony/NewsCommunity-bFinal/actions))

#### 7. 테스트 코드 작성
> - 특이사항 없음

#### 8. 프론트앤드를 위해 예외 관련 모든 response에 에러 코드를 넣어주고, API에 명시
> - [API 명세서](https://github.com/2022-Harmony/NewsCommunity-bFinal/wiki/API-%EB%AA%85%EC%84%B8%EC%84%9C)


*****
### 🩺 트러블 슈팅

#### 1. 작업 공간을 어떻게 나누어야 하는가
> - 기존 1차 프로젝트에선, 프론트 관점의 페이지 기준으로 작업 환경을 나눔 (ex. main, detail, login)
> - 이 경우, 개발인원들이 백앤드 리소스(DB 컬럼, 도메인 등..)를 중복해서 관리하게 되어 책임소재 복잡, 잦은 충돌 발생등의 문제가 생김
> - 작업 환경을 백앤드 관점의 도메인 기준으로 나누어 책임 소재를 명확히하고, 충돌이 발생 여지를 없앰.
> - (TradeOff) 프론트앤드에서 url 호출이 많아졌으며, 프론트앤드 관점에서는 페이지 기준으로 작업을 할당해야 충돌이 발생하지 않음
> - [자세히 보기](https://blog.naver.com/cksgurwkd12)


#### 2. JSON XSS 방어
> - `lucy-xss-servlet-filter` 를 이용해 XSS를 방어하려는 첫 번째 시도가 있었으나
> - 프론트에서 넘어오는 reqeust body가 JSON 형태로 이루어져, lucy-xss-servlet-filter를 적용 불가

#### 3. 슬로우 쿼리 발견 및 개선

#### 4. UUID 사용으로 발생한 조회 성능 이슈, 인덱싱을 통해 해결

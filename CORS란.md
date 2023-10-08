# CORS (Cross-origin-resourse-sharing)
--- 

예시: `https://domain-a.com`의 프론트 엔드 Javascript 코드가 XMLHttpRequest를 사용하여 `https://domain-b.com/data.json`을 요청하는경우

보안 상의 이유로 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청을 제한한다. 예를 들어, `XMLHttpRequest`와 Fetch와 같은 API는 동일 출처 정책(Same-ogrigin)을 따른다. 이 API를 사용하는 웹 애플리케이션은 자신의 출처와 동일한 리소스만 불러올 수 있으며, 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해야한다.

> Javascript 코드가 있는 서버가 아닌 다른 외부서버에 비동기로 리소스를 호출하면 외부 서버에서는 올바른 CORS 헤더를 포함해서 응답을 반환해야 브라우저에서 막지 않는다.

CORS 메커니즘은 브라우저와 서버 간의 안전한 교차 출처 요청 및 데이터 전송을 지원 한다. 최신 브라우저는 XMLHttpRequest 또는 Fetch와 같은 API에서 CORS를 사용하여 교차 출처 HTTP 요청의 위험을 완화한다.

---
## CORS를 사용하는 요청
- 위에 기재한 바와 같이, XMLHttpRequest와 Fetch와 같은 API호출.
- 웹 폰트(css 내 `@font-face`에서 교차 도메인 폰트 사용 시)를 사용하여 서버가 출처를 교차하여 로드할 수 있고 허용된 웹사이트에서만 사용할 수 있는 트루타입 글꼴을 배포할 수 있도록 한다.
## nodejs

서버 - 클라이언트가 요청하는 내용을 전달해주는 역할을 함
- 요청(CRUD)을 받으면 요청한 내용을 보내주는 프로그램

ex)
어떤 사람이 comic.naver.com으로 접속하면
네이버웹툰 메인 html파일을 전송해주세요

요청은 4개의 방식이 존재
1. get요청 - 읽기 요청
2. post요청 - 읽기 or 쓰기(생성) 요청
ex) 댓글 작성 및 블로그 포스트 작성
3. put요청 - 수정요청
4. delete요청 - 삭제요청

node js를 이용해 js문법으로 개발

node.js ?

javaScript
html에 종속된 언어.
html을 조작하기 위해 만들어진 언어
html : 웹페이지에 글쓰고 그림을 넣는 언어
js : 웹페이지를 다이나믹하게 바꿔주기가 가능
javascript의 해석은 브라우저가 담당
js해석 엔진이 브라우저에 내장되어있음.
Chrome - v8
firefox - spidermonkey
ie - chakra

v8엔진 떼어와 살을 붙여
브라우저 내에서 말고도 다른 환경에서도 js를 실행가능하게 만듬.

node js로 서버를 만들기가 가능

node js의 특징
event-driven, non-blocking I/O
non-blocking i/o
요청을 미리 다 받은 후 빨리 처리가 되는 순서대로 결과를 가져다줌.

node js의 강점
sns, 채팅서비스
특징 : 요청이 매우 많음
요청이 많아도 멈추거나 요청, 대기시간이 적음

일반 서버도
서버스케일링, 멀티쓰레딩으로 빠른 처리가 가능하긴 하다

node js는 코드가 짧고 쉬워 빠른 개발 가능
웹서비스 개발에 많이 쓰임.
이미지 처리 서버가 있어야 한다면 조금은 비효율적.

rest api
application programming interface
api규약에 따라 데이터를 전달

웹 개발 시 api란 무엇인가
서버와 고객간의 소통방식 (요청방식)
어떻게 해야 서버와 통신을 할 수 있을까

rest api
roy fielding이
http 요청 시스템
rest 원칙에 의해서 쓰자!라고 논문을 작성

restful한 프로그래밍을 위한 rest원칙 6개
1. Uniform interface
- 하나의 자료는 하나의 url로
url하나를 알면 둘을 알 수 있어야함

2. Client-Server 역한 구분
- 브라우저는 요청만 서버는 응답만

3. Stateless
- 요청들은 의존성이 없어야함

4. Cacheable
캐싱이 가능

5. Layered System
6. Code on Demand

ex)
www.example.com/products/66432
instagram.com/explore/tags/kpop/

url만 보고도 예측이 쉽게 가능함. - 간결




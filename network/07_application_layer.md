# 모두의 네트워크 #07_응용 계층: 애플리케이션에 데이터 전송하기

## lesson_28 응용 계층의 역할
- 애플리케이션이 동작하는 layer
- TCP/IP protocol :: (seesion layer + presetation layer + application layer) = application layer
- 통신대상이 이해할 수 있는 데이터로 변환하여 transport layer로 전송

## lession_29 웹 서버의 구조
- www == web 기술은 HTML, URL, HTTP 세가지 기술이 사용된다
  - HTML
    - 하이퍼텍스트
      - 문자, 이미지, 하이퍼링크를 표시
        - 하이퍼링크: link
    - 마크업 언어
      - 문장의 이룹를 태그로 감싸로 문장을 꾸미기 위한 형식
  - HTTP
    - HTTP/1.0 매 요청마다 새로운 연결
    - HTTP/1.1
      - keepalive: 데이터 교환을 마칠 때까지 연결 유지
      - 요청 처리가 순차적
    - HTTP/2
      - 요청 처리가 async
    
## lesssion_30 DNS 서버의 구조
- DNS
  - url -> ip
  - DNS 서버는 전세계에 흩어져 있고 모두 계층적
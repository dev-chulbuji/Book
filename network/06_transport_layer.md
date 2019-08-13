# 모두의 네트워크 #06_전송 계층: 신뢰할 수 있는 데이터 전송하기

## lesson_23 :: 전송 계층의 역할
- physical layer, data link layer, network layer를 통해 목저지에 데이터를 보낼 수 있다.
- transport layer은 목전지에 신뢰할 수 있는 데이터를 전달하기 위해 필요하다
  - error detecting -> automatic repeast request
  - decapsulation 과정에서 해당 데이터를 어떤 application 으로 보낼지 식별
- TCP(connection-oriented service), UDP(connectionless service) protocol
  - connection-oriented service: 신뢰성 / 정확성
  - connectionless service: 효율성

## lesson_24 :: TCP 구조
- TCP로 데이터를 전송할 때 transport layer의 capsulation단계에서 tcp header를 붙인다.
  - tcp header가 붙은 데이터: sagment
  - ```
    [source port][des port][sequence num][ACK num][header length][reserved bit][code bit][window size][check sum][urgent point][options]
    ```
  - connection-oriented service는 데이터를 보내기지 전에 connection 이라는 가상의 독점 통신로 확보를 한다.
    - `3-way handshake`
    - tcp header의 code bit를 사용한다.
    - tcp header code bit
      - ```
        [URG][ACK][PSH][RST][SYN][FIN]
        ```
    - connection을 맺기위해서는 code bit 중 SYN, ACK를 사용 `3-way handshake`
      - ```
        com1 ---> (SYN:1) ---> com                 // 연결요청
        com1 <--- (SYN:1, ACK:1) <--- com2         // 허가 & 연결요청
        com1 ---> (ACK:1) ---> com2                // 허가
        ```
    - connection 끊기 위해 code bit 중 FIN, ACK 사용
      - ```
        com1 ---> (FIN:1) ---> com2
        com1 <--- (ACK:1) <--- com2
        com1 <--- (FIN:1) <--- com2
        com1 ---> (ACK:1) ---> com2
        ```

## lesson_25 :: 일련번호와 확인 응답 번호의 구조         
- 일련번호(Sequence Number): 송신측에서 수신측에 이 데이터가 몇번째 데이터인지 알려주는 역할
- 확인 응답 번호(Ack Number): 어느 Sequence Number에 맞는 데이터를 수신했는지 응답
- ```
  com1 -> (SN:3001, AN:4001) -> com2
  com1 <- (SN:4001, AN:3201) <- com2
  com1 -> (SN:3201, AN:4001) -> com2
  ```
- SN, AN을 통해 데이터 손상 및 유실된 경우 재전송한다 (재전송 제어)
- window size
  - 매번 segment 하나를 보낼 때마다 확인 응답을 받으면 비효율
  - 3-way handshake때 받은 수신측의 window size만큼 segment를 보내고 이후에 응답을 받는다.
  - 즉, window 사이즈는 데이터를 받는 buffer size

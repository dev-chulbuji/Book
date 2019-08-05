# 모두의 네트워크 #02_네트워크_기본규칙
- protocol
  - 컴퓨터간 데이터를 주고 받을 때는 규칙
- OSI 모델
  - ISO에서 정의한 국제 통신 표준 규악. 네트워크 기본 구조를 일곱개 계층으로 나눠서 표준화한 통신 규약.
- TCP/IP 모델
  - OSI 7 layer -> 4 layer로 단순화 시켜 사용하는 모델. 인터넷 모델
- TCP/IP 모델에서 데이터 송신측은 capsulation을 통해 header정보가 포함된 데이터를 수신측으로 보내고 수신측 decapsulation을 통해 데이터를 수신한다.
  - capsulation: 상위 계층의 통신 프로토콜 정보를 데이터에 추가하여 하위 계층으로 전송시키는 기술
  - decapsulation: 그 반대
  - ```
    [date link layer header][network layer header][transport layer header][data][data link layer trailer]
    ```
- VPN
  - Virtual Private Network
  - 가상 통신 터널을 만들어 거점간 연결, 원격 접속
  - 인터넷 VPN  
    - 인터넷망 사용
    - 거점간 접속은 IPSec 암호 기술 프로토콜을 사용
    - 원격 접속은 암호화된 통신로를 만듬
  - IP-VPN
    - MPLS을 통해 통신 사업자 전용 폐쇄망을 사용. -> 암호화 필요 없음
    
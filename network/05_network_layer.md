# 모두의 네트워크 #04_데이터 링크 계층: 랜에서 데이터 전송하기
- data link layer는 네트워크 장비 간에 신호를 주고받는 규칙(보통, 이더넷)을 정한다.
- 이더넷은 랜에서 데이터를 정상으로 주고받기 위한 규칙
- 이더넷을 통해 랜으로 데이터를 보낼 때 패킷간 충돌이 일어날 수 있다
- 초기에는 CSMA/CD 라는 이더넷에서 시점을 늦추는 방법으로 충돌을 해결했다.
  - CSMA/CD (Carrier Senese Multiple Access with Collision Detection)
    - 'CS' 데이터를 보내려고 하는 컴퓨터가 케이블에 신호가 흐르고 있는지 확인하는 규칙
    - 'MA' 케이블에 데이터가 흐르고 있지 않다면 데이터를 보내도 좋다는 규칙
    - 'CD' 충돌이 발생하고 있는지를 확인하는 규칙
- data link layer에서는 capsulation 과정에서 이더넷 header와 data 끝에 trailer를 붙여 frame을 만들고 physical layer에서는 frame을 전기신호로 변환하여 데이터를 전송한다.
- data link layer의 capsulation 과정에선 header로 출발지, 목적지 정보를 담는다.
  - 이때 출발지, 목적지 주소는 MAC Address를 사용한다.
    - MAC Address는 랜 카드가 생성될 때 전세계 유일한 고유 번호를 할당 받는 것으로 총 48bit다 (앞 24bit는 제조사, 뒤 24bit는 일련번호)
- data link layer의 capsulation 과정에선 header 정보로는 [목적지 MAC][출발지 MAC][Ethernet type]
  - Ethernet type은 이더넷으로 전송되는 상위 계층 프로토콜의 종류 (IPv4, IPv6, ARP, RARP, SNMP)
    - APR
      - 목적지 ip를 이용하여 MAC address를 찾기 위한 프로토콜
      - 데이터를 보낼 때 목적지 MAC address를 모를 때 네트워크에 broadcast를 하여 목적지 컴퓨터로 부터 MAC address를 받는다.
      - 받은 목적지 MAC address는 ARP table에 caching 주기를 가지고 저장을 하고 다음 통신 때 활용한다.
- data link layer의 capsulation 과정에선 header외에 data에 trailer를 붙이는데 이건 FCS(Frame Check Sequence)로 전송 도중 오류 발생 여부 판단 용도이다.
- frame = [data link layer header][data][trailer]

## 허브를 통한 통신
  - 기존에 hub에 물려있는 여러 컴퓨터는 hub의 특성상 packet을 보낸 컴퓨터를 제외하고 연결된 모든 컴퓨터에 broadcast를 하는 형태로 통신이 이뤄진다.
  - 데이터를 받은 컴퓨터는 physical layer에서 전기신호 -> 비트열, data link layer에서 decapsulation 과정으로 header의 정보를 보고 자신의 mac address가 아니면 파기한다.
  - hub를 통한 통신에선 충돌을 방지하기 위해 CSMA/CD

## 스위치를 통한 통신
  - 스위치는 data link layer에서 동작하고 L2 switch or switching hub라고 불린다.
  - 스위치 내부에는 MAC address table(bridge table)라는 (port와 MAC address) 데이터가 있는 database가 있다.
  - learning
    - 처음에 switch의 bridge table은 비어있는 상태이다.
    - 컴퓨터에서 데이터가 전송이 되면 MAC 주소 테이블을 확인하고 출발지 MAC 주소가 등록되어 있지 않으면 추가하는 것
  - flooding
    - 아직 목적지 MAC address가 bridge table에 등록되어 있지 않으면 나머지 포트에 데이터를 전송한다.
    - 목적지 컴퓨터는 ACK로 자신의 MAC address를 bridge table에 등록시키도록 한다.
  - filtering
    - bridge table에 등록되어 있는 MAC address일 경우 flooding을 하지 않는다.
  
ㄷ# 모두의 네트워크 #05_네트워크 계층: 목적지에 데이터 전달하기

## lesson_17 :: 네트워크 계층의 역할
- 같은 LAN끼리는 data layer만으로 MAC address를 통해 통신을 할 수 있다.
- 네트워크가 다른(분리된) 환경에서 네트워크간 통신을 하기 위해 network layer가 필요하다.
  - 네트워크간 통신은 router라는 장비를 통해 이뤄진다.
  - 네트워크간 통신은 같은 LAN에서는 MAC Address로 가능하지만 다른 네티워크 끼리의 통신은 IP(Internet Protocol)이 필요하다.
  - IP를 통해 목적지를 지정하는 것 뿐만 아니라 routing 즉, 어떤 경로로 보낼지도 결정해야 한다.
  - 라우팅은 router 장비가 그 역할을 맡는다 (L3 스위치도 라우팅 기능이 있다.)
  - router는 routing table을 참조하여 routing 한다.
- network layer의 대표적인 프로토콜인 IP
  - network layer에서 capsulation 단계에서 ip header를 붙인다.
  - ```  
     [version]]header-length][service-type][total-length][ID][flags][fragment offset][TTL][protocol][header-checksum][source-IP][destination-IP]
    ```
  - ip header가 capsulation된 데이터를 IP p/acket이라 부른다.

## lesson_18 :: IP 주소의 구조
- IP address는 ISP로 부터 받을 수 있으며 IPv4(32bit), IPv6(128 bit) 2가지가 있다.
- IP address는 공인 IP, 사설 IP가 있다.
- IPv4는 32bit로 약 43억개의 ip를 할당할 수 있는데 -> 부족 -> (공인IP & 사설IP로 나눔 or IPv6)
- 공인IP는 router에만 할당을 하고 LAN안에 있는 컴퓨터들에게는 DHCP를 활용하거나 사설 IP주소를 할당한다.
  - DHCP(Dynamic Host Configuration Protocol)는 IP주소를 자동으로 할당하는 프로토콜이다.
- IP주소는 8bit씩 나눠서 표기하며 8bit을 옥텟(octet)이라 부른다.
- IPv4에서 IP 주소는 networkID와 hostID로 나눠진다.
  - networkID: 어떤 network인가?
  - hostID: 해당 네트워크의 어떤 컴퓨터인가?

## lesson_19 :: IP 주소의 클래스 구조
|class | content | networkID bit | hostID bit | networkID 범위 |
|------|:------------------:|:---:|:---------:|--------------:|
|A class | 대규모 네트워크 주소 | 8bit | 24bit | 1 ~ 127 |
|B class | 중용 네트워크 주소 | 16bit | 16bit | 128 ~ 191 |
|C class | 소형 네트워크 주소 | 24bit | 8bit | 192 ~ 223 |
|D class | muticast 주소 |
|E class | 연구 및 특수용도 주소 |

- 위 표는 각 클래스별 전체 ip address 범위를 나타낸 것
- 각 클래스별 공인ip, 사설ip 주소는 범위는 따로 있다.

## lesson_20 :: 네트워크 주소와 브로드캐스트 주소의 구조
- network address와 broadcast address는 컴퓨터에 할당할 수 없다.
  - C 클래스의 경우 network address는 hostID가 0 (00000000)
  - C 클래스의 경우 broadcast address는 hostIDrk 255 (11111111)
- network address
  - network address는 전체 network에서 작은 network를 식별하는 데 사용
  - network address는 해당 네트워크 전체를 대표하는 주소
    - 192.168.1.1의 ip 주소를 가진 컴퓨터는 192.168.1.0의 network에 속한다라고 이야기 할 수 있다.
- broadcast address
  - network내 모든 장비에게 한번에 데이터를 전송하기 위한 ip

## lesson_21 :: 서비넷의 구조
- subnetting: 대규모 네트워크를 작은 네트워크(subnet)로 분할
- ip 주소의 부족, 낭비 -> subnetting
- 많은 수의 장비가 하나의 network로 묶여 있으면 broadcast시 엄청 비효율적임
- subnetting되면 ip주소 체계가 기존의 networkID와 hostID -> networkID, subnetID(기존에 hostID), hostID로 나누어진다.
- 서브넷 마스크: 어디까지 networkID이고 hostID인지 표기 
  - 서브넷 마스크가 255.255.255.240 (11111111.11111111.11111111.11110000) -> /28

## lesson_22 :: 라우터의 구조
- 서로 다른 network끼리 통신하기 위해선 router가 필요 -> 즉, router를 통해 network를 분리할 수 있다.
- 반면 스위치(L2 스위치)만으론 네트워크를 분리할 수 없다. (=허브)
- 네트워크 1(192.168.1.0/24)의 a컴퓨터에서 네트워크2(192.168.2.0/24)의 b컴퓨터로 데이터를 전송하고 싶다면
  - router의 ip 주소를 설정 = default gateway 설정 (192.168.1.1)
  - router는 routing protocol을 통해 router간 서로 routing 정보를 교환하여 routing table에 저장한다.
    - routing protocol : RIP, OSPF, BGP
  - a컴퓨터에서 default gateway로 데이터를 전송하면 router에서 routing table을 참조하여 network2의 router로 전달하고 network2의 switch가 컴퓨터2로 데이터 전송
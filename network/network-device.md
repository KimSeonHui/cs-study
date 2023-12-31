<div align=center>
  <h1> network device 😺 </h1>
</div>

> 발표일　　|　 2023.10.11 <br />
> 발표자　　|　강준영 <br />

<div align=center>
  <h3>📇 목차 </h3>
</div>

[1. 정의](#🏭-정의)<br />
[2. Application](#🌊-Application)<br />
[3. Network](#🦴-Network) <br />
[4. DataLink](#🧩-DataLink) <br />
[4. Physical](#🧩-Physical) <br />

<br>

# 🏭 정의

네트워크는 여러가지의 기기를 기반으로 구축됩니다.

계층별로 처리 범위를 나눈다면

```
Application Layer : L7 Switch
Network Layer : L3 Switch
Data Link Layer : Bridge, L2 Switch
Physical Layer : NIC, Repeater, AP

```

로 나눌 수 있습니다.

상위 계층은 하위 계층을 처리할 수 있지만, 그 반대로는 불가능합니다.

(ex : L7 Switch 는 모든 게층의 프로토콜 처리 가능, but AP는 Physical Layer만 처리 가능)

※ switch : 여러 장비를 연결하고 데이터 통신을 중재하며 목적지가 연결된 포트로만 전기 신호를 보내 데이터를 전송하는 통신 네트워크 장비.

<br>

# 🌊 Application

### L7 Switch

```
- 로드밸런서

- 클라이언트로 오는 요청들을 뒤 쪽 여러 서버로 나누는 역할

- 서버의 부하를 분산하여 처리 가능한 트래픽을 증가시키는 것을 목표로함. (URL, 서버, 캐시, 쿠키를 기반으로 트래픽 분산)

- 바이러스, 불필요한 외부 데이터 필터링

- 응용 프로그램 수준의 트래픽 모니터링 가능

- 장애가 발생한 서버가 있다면 트래픽 분산 대상에서 제외해야함 -> 정기적으로 health check를 이용하여 감시.
```

※ health check :

서버가 정상적인지에 대한 여부를 판별하는데 사용되는 방법.

전송 주기와 재전송 횟수등을 설정하고 반복적으로 서버에 요청을 보내는 방식

TCP, HTTP등 다양한 방법으로 요청 보내고 응답이 정상적이라면 정상 서버로 판별

if TCP 요청 보냈는데 3-way handshake 정상x -> 비정상 판별

서버가 부하되지 않을 만큼 요청 횟수를 적절하게 설정해야함. (일반적으로 5~30초 사이)

### L7 vs L4 Switch

```
L4 Switch 역시 로드 밸런서. (Transport Layer)

둘의 차이점은 트래픽을 분산하는 방법.

- L4 Switch : IP와 포트를 기반으로 트래픽 분산(Network Load Balancer)

- L7 Switch : IP, 포트 이외에도 URL, HTTP 헤더, 쿠키 등을 기반으로 트래픽 분산. ALB(Application Load Balancer)



```

# 🦴 Network

## Router

- 라우팅

  ```
  여러개의 네트워크를 연결, 분할, 구분하는 역할

  다른 네트워크에 존재하는 장치끼리 데이터를 서로 주고 받을 때, 패킷 소모를 최소화하고 경로를 최적화하여 최소 경로로 패킷을 포워딩.
  ```

## L3 Switch

- L2 Switch의 기능 + 라우팅 기능을 모두 갖춘 장비.

※ 참고

| 구분        | L2 스위치       | L3 스위치     |
| ----------- | --------------- | ------------- |
| 참조 테이블 | MAC 주소 테이블 | 라우팅 테이블 |
| 참조 PDU    | 이더넷 프레임   | IP 패킷       |
| 참조 주소   | MAC 주소        | IP 주소       |

# 🧩 DataLink

## L2 Switch

```
MAC 주소 테이블을 통해 장치들의 MAC 주소 관리

패킷이 왔을 때, 패킷 전송.

IP 주소를 이해하지 못한다는 특징을 가지고 있어서 IP 주소 기반 라우팅은 불가능.

단순히 패킷의 MAC주소를 읽어 스위칭 하는 역할

목적지가 MAC 주소 테이블에 없다면 전체 포트를 전달하고 MAC 주소 테이블의 주소는 일정 시간 이후 삭제하는 기능이 있음.
```

## Bridge

```
두 개의 근거리 통신망 (LAN)을 상호 접속할 수 있도록 하는 통신망 연결장치.

포트와 포트 사이의 다리 역할
장치에서 받아온 MAC 주소를 MAC 주소 테이블로 관리

브리지는 통신망 범위를 확장하고 서로 다른 LAN등으로 이루어진 하나의 통신망을 구축할 때 사용
```

# 🧩 Physical

## NIC

```
Network Interface Card의 약자. LAN 카드임.

네트워크와 빠른 속도로 데이터를 송수신할 수 있도록 컴퓨터 내에 설치하는 확장 카드.

각 LAN 카드에는 주민번호처럼 구분하기 위한 고유 식별 번호인 MAC 주소 있음.
```

## Repeater

```
들어오는 약해진 신호를 증폭하여 다른 쪽으로 전달하는 장치

신호 간섭 문제 발생 가능.. -> 성능 저하

패킷이 더 멀리 가게 해주지만 광 케이블이 보급됨에 따라 현재는 잘 사용 x, AP나 Mesh 네트워크 기술을 사용.
```

※ Mesh 네트워크 기술
노드 간 서로 연결되어 있어 데이터를 전송할 때 최적 경로를 찾아 전달할 수 있는 네트워크 기술.

각 노드는 인접 노드와 통신하여 데이터를 전달하는 역할도 하고 Relay 하는 역할도 수행.

확장성 향상, 크고 복잡한 환경에서 유용.

(활용 분야 : IoT, 스마트 홈, 스마트 빌딩)

## AP

```
Access Point의 약어.

무선 네트워크 환경에서 유선 네트워크와 무선 디바이스 간 통신을 가능하게 하는 역할.
```

#### 출처

1. [CS 스터디] 2.3 네트워크 기기 : https://velog.io/@devroomie/CS-%EC%8A%A4%ED%84%B0%EB%94%94-2.3-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EA%B8%B0%EA%B8%B0

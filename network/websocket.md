# Web Socket
## Web Socket 등장 배경
기본적으로 클라이언트와 서버는 http / https 통신으로 stateless하게 이루어져 있고 클라이언트에서 Request를 하면 서버에서는 Response하는 과정으로 이루어져 있다.

![image](https://github.com/KimSeonHui/cs-study/assets/44824456/c58abdae-d8bd-4f43-8778-21112d2b5b84)

> 사용자가 URL을 요청할 때만, 서버에서 해당 페이지 결과를 받을 수 있다.   
즉, **사용자는 서버로부터 새로운 정보를 받기 위해서는 반드시, 새로운 URL을 요청해야 한다는 것이다.** 

<br >

- 초창기 웹 :: 사용자와 상호작용은 크게 중요하지 않음
- 사용자과의 인터렉션이 증가하게 되면서 서버와 클라이언트 간의 상호작용이 중요하게 됨
- HTTP 방식은 실시간 웹 서비스를 만드는 게 복잡하고 어려워짐
    - 반드시 요청을 해야만 응답을 받아야 하기 때문에!
- 불편함을 개선하고 실시간 상호작용 하는 웹 페이지를 더 쉽게 만들 수 있도록 HTML 5 표준으로 웹소켓 API가 등장

<br ><br >

## Web Socket 이전에 비슷한 기술
> 웹 소켓 이전 기술들은 클라이언트 → 서버로 단방향 통신 프로토콜인 Http 통신에 약간의 트릭을 사용해서 마치 실시간인 것처럼 작동함

<br >


### 1. Polling
> 서버로 일정 주기마다 http 요청을 하는 방식    

![image](https://github.com/KimSeonHui/cs-study/assets/44824456/a33ac547-20ce-432c-8db9-66e3fb26781f)


- 가장 간단한 방법
- 언제 통신이 발생할지 예측이 불가능하기 때문에 클라이언트가 http request를 일정한 주기로 서버에 요청해 응답을 전달받는 방식
-  언제 통신이 발생할지 예측이 불가능해 클라이언트가 주기적으로 요청을 하기 때문에 클라이언트가 많아지면 서버의 부담이 급증
- 실시간 정도의 빠른 응답 X

<br >


### 2. Long Polling
> 서버로 http 요청을 한 후 응답이 있을 때만 서버가 response를 클라이언트로 전달하는 과정을 반복

![image](https://github.com/KimSeonHui/cs-study/assets/44824456/2095c4de-6e84-4db4-ac3d-1151c4e876ad)

- Polling과 비슷하지만 실시간 데이터 처리할 수 있는 방식
- 일반 Polling과 비교했을 때 서버의 부담이 줄어듬
- 클라이언트에게 동시에 많은 양의 메세지가 올 경우 Polling과 별 차이가 없게 되고, 다수의 클라이언트에게 동시에 요청이 발생될 경우 서버로 여러 접속이 시도하게 되면서 서버의 부담이 급증하게 됨

<br >

### 동작 방식
1. 클라이언트에서 서버로 http 요청을 보내고 서버에서 응답이 올 때까지 계속 대기
2. 서버는 해당 클라이언트로 전달할 응답이 있을 때 response를 전달하고 연결을 종료
3. 연결이 종료된 이후에는 클라이언트에서 곧바로 다시 http 요청을 보내 다음 응답을 기다림

<br >


### 3. Streaming
> 클라이언트와 서버 간 연결 된 연결 통로로 데이터를 보내는 방식

![image](https://github.com/KimSeonHui/cs-study/assets/44824456/d7218362-9cbf-48ba-8b85-2ff7008cf345)

- 서버에서 메세지를 보낸 후 다시 http 요청을 연결하지 않아도 되어 Long Polling이 비해 부담이 덜함

<br >

### 동작 방식
1.  처음에 클라이언트에서 서버로 http 요청을 보냄
2. 서버에서 클라이언트로 응답을 전달할 때, 해당 요청을 끊지 않고 필요한 메세지만 보냄

<br ><br >


## Web Socket이란?
- 웹 소켓 HTML5 표준 기술로 두 프로그램 간의 메세지 교환을 위한 통신 방법 중 하나
- WebSocket API를 통해 서버로 메세지를 보내고, 요청 없이 응답을 받아오는 것이 가능

<br >

### 특징

**1.양방향 통신**
- 하나의 커넥션으로 데이터 송수신을 동시에 처리할 수 있는 통신 기법
- 클라이언트와 서버가 서로에게 원할 때 데이터를 주고 받을 수 있음


**2.실시간 네트워킹**
- 웹 환경에서 연속된 데이터를 빠르게 노출할 수 있음   
  ex) 채팅, 주식, 비디오

  <br >


### 웹 소켓 동작 방법
웹 소켓은 핸드 쉐이킹에 Socket 프로토콜이 아니라 http/https 프로토콜로 이뤄짐

> **핸드 쉐이킹(Hand Shaking)이란?**   
정상적인 통신이 시작되기 전에 두 채널이 서로 연결 될 때 필요한 정보들을 주고받는 과정들

![image](https://github.com/KimSeonHui/cs-study/assets/44824456/e3bbfe64-70c2-4389-a176-c803fc0f4213)


#### **웹 소켓 요청**   
| - http 버전은 1.1이상    
| - 반드시 GET 메서드 사용해야 함    
| - Upgrade 정보는 서버, 전송, 프로토콜 연결에서 다른 프로토콜로 업그레이드 / 변경하기 위한 규칙  
| - Sec-Websocket-Key는 클라이언트가 요청하는 여러 서브 프로토콜 의미

<br >

#### **웹 소켓 응답**   
| - 101 Switchiing Protocols가 response로 오면 웹소켓이 연결된 것  
| - Sec-Websocket-Accept는 요청에서의 Key값을 계산한 값으로 신원 인증에 필요한 헤더

<br >


핸드 쉐이크가 완료되면 프로토콜이 ws로 변경됨
- ssl이 적용된 프로토콜은 wss로 변경됨

![image](https://github.com/KimSeonHui/cs-study/assets/44824456/f5007e52-37bf-4527-b908-539a54872249)


<br >

### 웹 소켓 프로토콜 특징
- 최초 접속 시에만 http 프로토콜 위에에서 핸드쉐이킹을 하기 때문에 http header를 사용
- 웹 소켓을 위한 별도의 포트 없이 기존 포트를 사용
- 프레임으로 구성된 메세지라는 단위로 송수신
- 메세지에 포함될 수 있는 교환 가능한 메세지는 텍스트와 바이너리 뿐

<br >

### 웹 소켓 한계
**1. HTML5에서 표준으로 등장한 기술**    
- 웹소켓은 HTML5에서 표준 기술로 등장했기 때문에 HTML5 이전 기술로 구현된 서비스에서는 웹 소켓을 사용할 수 없음


**2. WebSocket은 문자열을 주고 받을 수 있는 역할만 함**   
- http는 주고 받는 메세지 형식이 모두 정해져 있어 모두가 약속을 따르면 쉽게 해석할 수 있음
- WebSocket의 경우 형식이 정해져 있지 않아 어플리케이션에서 쉽게 해석하기 힘듬
- WebSockeet 방식을 sub-protocols를 사용해 주고 받는 메세지의 형태를 약속하는 경우가 많음

<br ><br >

## 참고 자료
- [웹 소켓 정리(역사부터 차근차근)](https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-%EC%9B%B9-%EC%86%8C%EC%BC%93-Socket-%EC%97%AD%EC%82%AC%EB%B6%80%ED%84%B0-%EC%A0%95%EB%A6%AC#%EC%9B%B9_%EC%86%8C%EC%BC%93_%EC%9D%B4%EB%9E%80?)
- [Web Socket의 개념 및 사용 이유, 작동원리, 문제점](https://choseongho93.tistory.com/266)
- [Web Socekt이란?](https://velog.io/@codingbotpark/Web-Socket-%EC%9D%B4%EB%9E%80)
- [Polling / Long Polling / Streaming](https://velog.io/@hahan/Polling-Long-Polling-Streaming)
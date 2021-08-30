# Socket

## 소켓이란?

- 프로세스가 드넓은 네트워크 세계로 데이터를 내보내거나 혹은 그 세계로부터 데이터를 받기 위한 실제적인 창구 역할
- 프로세스가 데이터를 보내거나 받기 위해서는 반드시 소켓을 열어서 소켓에 데이터를 써보내거나 소켓으로부터 데이터를 읽어들여야 한다.

소켓은은 프로토콜, IP 주소, 포트 넘버로 정의된다.

- 프로토콜

    프로토콜은 원래 외교상의 언어로써 의례나 국가간에 약속을 의미하며, 통신에서는 어떤 시스템이 다른 시스템과 통신을 원활하게 수용하도록 해주는 통신 규약, 약속

- IP

    전 세계 컴퓨터에 부여된 고유의 식별 주소

- 포트

    포트(Port)는 네트워크 상에서 통신하기 위해서 호스트 내부적으로 프로세스가 할당받아야 하는 고유한 숫자이다. 한 호스트 내에서 네트워크 통신을 하고 있는 프로세스를 식별하기 위해 사용되는 값이므로, 같은 호스트 내에서 서로 다른 프로세스가 같은 포트 넘버를 가질 수 없다. 즉, 같은 컴퓨터 내에서 프로그램을 식별하는 번호이다.

## 흐름

![Socket%206a7b44ef22954a2e89b77cd30bfdb053/Untitled.png](image/socket.png)

**서버 (Server)**

클라이언트 소켓의 연결 요청을 대기하고, 연결 요청이 오면 클라이언트 소켓을 생성하여 통신이 가능하게 한다

1) socket() 함수를 이용하여 소켓을 생성

2) bind() 함수로 ip와 port 번호를 설정하게 됩니다.

3) listen() 함수로 클라이언트의 접근 요청에 수신 대기열을 만들어 몇 개의 클라이언트를 대기 시킬지 결정

4) accept() 함수를 사용하여 클라이언트와의 연결을 기다림

**클라이언트 (Client)**

실제로 데이터 송수신이 일어나는 것은 클라이언트 소켓이다.

1) socket() 함수로 가장먼저 소켓을 연다.

2) connect() 함수를 이용하여 통신 할 서버의 설정된 ip와 port 번호에 통신을 시도

3) 통신을 시도 시, 서버가 accept() 함수를 이용하여 클라이언트의 socket descriptor를 반환

4) 이를 통해 클라이언트와 서버가 서로 read(), write() 를 하며 통신 (이 과정이 반복)

## 종류

1. TCP
2. UDP

## HTTP 통신과 SOCKET 통신 비교

**HTTP 통신**

- Client의 요청(Request)이 있을 때만 서버가 응답(Response)하여 해당 정보를 전송하고 곧바로 연결을 종료하는 방식

**HTTP 통신의 특징**

- Client가 요청을 보내는 경우에만 Server가 응답하는 **단방향 통신**이다.
- Server로부터 **응답을 받은 후에는 연결이 바로 종료**된다.
- 실시간 연결이 아니고, 필요한 경우에만 Server로 요청을 보내는 상황에 유용하다.
- 요청을 보내 Server의 응답을 기다리는 어플리케이션의 개발에 주로 사용된다.

**SOCKET 통신**

- Server와 Client가 특정 Port를 통해 실시간으로 양방향 통신을 하는 방식

**SOCKET 통신의 특징**

- Server와 Client가 **계속 연결을 유지**하는 양방향 통신이다.
- Server와 Client가 실시간으로 데이터를 주고받는 상황이 **필요한 경우**에 사용된다.
- 실시간 동영상 Streaming이나 온라인 게임 등과 같은 경우에 자주 사용된다.
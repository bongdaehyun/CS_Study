# OAuth

OAuth는 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준이다.

→ API를 이용해서 사용자의 정보를 다른 서비스를 통해 들고 오는 것

## 주요 용어

Resource Server : 정보가 저장되어있는 서버 (ex. facebook, google ..)

Resource Owner : Resource Server 에 저장 돼 있는 Resource(정보)의 주인(사용자)

Client : 우리가 만들자고 하는 Web 또는 App

## 동작

Client는 Resour Server에 등록해 Resource Server에게 Id와 secret을 발급받는다.

Resource Owner는 Client에게 자신의 정보를 제공해도 된다고 Resource Server에게 승인하면 Resource Server는 Client에게 Resource Owner를 식별해주는 authorization code를 발급해준다.

Client는 발급받은 Id, secret, code를 Resource Server에 전달해주면 Resource Server는 전달 받은 Id, secret, authorization code가 유효한지 확인한 후 검증서 역할을 하는 Access Token을 발급해준다.

이제 Client는 Resource Owner의 정보가 필요할 때마다 Resource Server에발급받은 Access Token을 보내 Resource Owner의 정보를 가져온다.
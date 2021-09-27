# DNS Round Robin

- 별도의 SW,HW로드벨런싱 장비 없이 오직 DNS만을 이용하여 도메인 레코드 정보를 조회하는 시점에서 트래픽을 분산하는 기법이다.
- 웹 뿐만 아니라, 도메인을 사용하는 모든 서비스(FTP,SMTP 등)에 사용이 가능하다.

## 원리

1. 웹서비스를 담당할 여러 대의 웹서버는 자신의 공인 IP를 각각 가지고 있다
2. 사이트 접속을 위해 사용자가 해당 도메인 주소를 브라우저에 입력하면 DNS는 도메인의 정보를 조회하는데 이때 IP주소를 여러 대의 서버 IP리스트 중에서 라운드 로빈 형태로 랜덤하게 하나 혹은 여러개를 선택하여 사용자에게 알려준다,.
3. 결과적으로 웹사이트에 접속하는 다수의 사용자는 실제로는 복수의 웹서버에 나뉘어 접속해도 되면서 자연스럽게 서버의 부하가 분산되는 방식

## 장점

1. 중간 장비(로드밸런서) 없이도 서비스가 가능
2. 비용적인 부분이 줄어듬
3. 간편하다

## 단점

1. 서버의 수만큼 공인 IP 주소가 필요합니다.
2. 균등하게 분산되지 않는다
3. 서버가 다운되도 확인이 불가능

## 극복 방법

- 다중화 구성방식
    - AP 서버에 VIP(Virtual IP)를 부여해서 다중화를 구성한다. 각 AP 서버를 Health Check후 이상이 감지되면 VIP를 정상 AP 서버로 인계하는 방식을 사용한다.즉 DNS Server Table 에 실시간으로 AP 서버의 상태를 확인할 수 있는 칼럼 및 함수를 추가하여 요청될 경우 서버 상태를 확인하여 우회루트를 제공하거나 에러를 전송하는 방식을 말합니다.
- 가중치 편성방식
    - 각각의 웹 서버에 가중치를 가미해서 분산 비율을 변경한다. 물론 가중치가 큰 서버일수록 빈번하게 선택되므로 처리능력이 높은 서버는 가중치를 높게 설정하는 것이 좋다.
- 최소연결 방식
    - 접속 클라이언트 수가 가장 적은 서버를 선택한다. 로드밸런서에서 실시간으로 connection 수를 관리하거나 각 서버에서 주기적으로 알려주는 것이 필요하다.
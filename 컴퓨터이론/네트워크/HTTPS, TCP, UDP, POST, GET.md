<aside>
💡 이 문서는 Post와 Get에 대하여 다루고있습니다.

</aside>

# 👀 Post와 Get의 공통점

> HTTP 프로토콜을 이용해서 서버에 무엇인가를 요청할 때 사용하는 방식이다.

---

# 👀 Post와 Get의 차이점

> GET

GET은 데이터를 요청 할 때 Header 부분에 url이 담겨 전송된다. url 상에 ? 뒤에 데이터를 붙어 request를 보내게 된다. 이런 GET방식은 url에 데이터를 담아 전달하기 때문에 데이터의 크기가 제한적이다. 또 url이 그대로 노출되므로 보안에 취약하다.

GET의 용도는 데이터를 가져오는 것이다. 서버의 값이나 상태를 변경하지 않는다.

> POST

POST는 데이터를 요청 할 때 Body 부분에 데이터가 담겨 전송된다. GET 방식에 비해서 데이터 크기에 제한이 적고 보안이 더 안전하다.

POST는 서버의 값이나 상태를 추가, 변경하기 위해 주로 사용된다.

> GET과 POST

GET 방식은 브라우저에서 Caching 할 수 있기 때문에 POST대신에 데이터가 작고 보안적인 문제가 없다는 이유로 GET 방식으로 요청을 하면 caching되었던 데이터가 응답이 될 가능성이 존재한다. 때문에 목적에 맞는 기술을 사용해야한다.

---

# 💭 TCP와 UDP

> TCP의 연결 방법과(3-way-handshake) 해제 방법(4-way-handshake)

- 연결 방법과(3-way-handshake)

Client → Server에게 접속 요청 SYN(a) 패킷을 보낸다.

Server는 Client 요청인 SYN(a)를 받고 Client에게 요청을 수락한다는 ACK(a+1)과 SYN(b)인 패킷을 발송한다.

Client는 Server의 응답인 ACK(a+1)과 SYN(b) 패킷을 받고 ACK(b+1)를 서버로 보내면 연결이 된다.

- 해제 방법(4-way-handshake)

Client → Server에게 접속 종료 FIN플래그를 보낸다.

서버는 Client 요청인 FIN을 받고 확인 메시지(ACK)를 보낸다. 그 후 데이터를 다 보낼 때까지 TIME_OUT된다.

데이터를 모두 보내고 통신이 끝났으면 연결이 종료되었다고 Client에게 FIN 플래그를 보낸다.

Client는 FIN을 확인했다면 ACK를 보낸다.

ACK 메시지를 받은 Server는 소켓 연결을 close한다.

Client는 서버로부터 받지 못한 데이터가 있을 것을 대비하여 일정 시간동안 세션을 남겨놓고 잉여 패킷을 기다린다 (TIME_WAIT)

> TCP

TCP는 서로 요청과 응답을 보내기 때문에 TCP 연결은 양방향성이다. Client ←→ Server 서로 존재를 알리고 패킷을 보낼 수 있다는 신호를 보내야한다. 그러므로 적어도 2-way-handshake로는 부족하다.

처음 SYN 포켓을 보낼 때 0부터 보내는게 아니라 난수로 보내는데 연결을 맺을 때 사용하는 Port는 유한 범위 내에 사용되고 시간에 따라 재사용되므로 두 통신 호스트가 과거에 사용된 포트 번호 쌍일 수도 있다. 서버는 패킷의 SYN을 보고 패킷을 구분하는데 난수가 아닌 순차적인 number가 발생 시 이전의 connection으로부터 오는 패킷으로 인식 할 수 있어서 가능성을 줄이기 위해 난수를 사용한다.

> TCP와 UDP

TCP와 UDP는 OSI 7 계층 중 Layer 4 : 전송계층에서 사용되는 프로토콜(컴퓨터 사이에서 메시지를 주고 받는 양식과 규칙의 체계)이다. 전송 계층은 프로토콜 내에 송수신자를 연결하는 통신 서비스를 제공하는 계층이다.

TCP는 신뢰성 있는 데이터 전송을 지원하는 연결 지향형 프로토콜이다. 보통 TCP와 IP가 함께 사용되고 IP는 데이터 전송, TCP는 패킷 추적 및 관리를 한다. TCP는 3-way-handshaking 과정을 통해 통신을 시작하고 흐름 제어(데이터 처리속도 차이 조절)과 혼잡 제어(패킷 수 넘침 방지)를 지원하며 데이터의 순서를 보장한다.

UDP는 비연결형 프로토콜로 서로 정보를 주고 받을 때 보내거나 받는 신호 절차를 거치지 않고 보내는 쪽에서 일반적으로 데이터를 전달하는 통신 프로토콜이다. TCP와 다르게 연결 설정이 없으며 혼잡 제어를 하지 않아 TCP보다 전송속도가 빠르다. 하지만 데이터 전송에 대한 보상을 하지 않아 패킷 손실이 발생할 수 있다.

TCP는 연속성보다 신뢰성 있는 전송이 중요할 때에 사용되는 프로토콜이며,UDP는 TCP보다 빠르고 네트워크 부하가 적다는 장점이 있지만 신뢰성 있는 데이터 전송을 보장하지는 않습니다.그렇기 때문에 신뢰성보다는 연속성이 중요한 실시간 스트리밍과 같은 서비스에 자주 사용됩니다.

---

# 💭 HTTP, HTTPS

> HTTP의 문제점

- 암호화가 안된 통신이라 도청 가능

TCP/IP 구조 통신은 경로를 엿볼 수 있고 패킷 수집만으로도 도청 가능한 네트워크다. 암호화 안 된 통신으로 메시지의 의미를 파악 할 수 있기 때문에 암호화를 해야한다.

- 통신 상대를 확인하지 않아 위장 가능

통신 상대를 확인하지 않아 누구든지 req를 보낼 수 있다. IP 주소, 포트 등에서 그 웹 서버에 액세스 제한이 없는 경우 req가 오면 상대가 누구든지 무언가의 response를 반환한다. 그러기 떄문에 어디에서 누가 req 했는지, 의미없는 req인지(Dos 방지), 웹이나 클라이언트가 의도한 res, req인지 알 수 없다.

- 완전성 증명할 수 없어 변조 가능

서버나 클라이언트에서 수신한 내용이 송신측에서 보낸 내용과 일치한다는 것을 보장할 수 없다. 그리하여 res, req후에 누가 변조하더라도 이 사실을 알 수 없다. 공격자가 도중에 req나 res를 빼앗아 변조하는 공격을 중간자 공격(Man-in-the-Middle)이라고 부른다.

위의 문제들은 암호화하지 않은 프로토콜도 해당된다.

> HTTPS

통신 자체를 SSL(Secure Socket Layer)나 TLS(Transport Layer Security)라는 프로토콜을 조합하여 HTTP를 암호화 할 수 있는데 SSL를 조합한 HTTP를 HTTPS라고 한다. 암호화해서 전송하면 받는 측에서는 해독하여 출력하는 처리가 필요하다. HTTPS는 통신하는 소켓 부분을 SSL, TLS라는 프로토콜로 대체한다. 그래서 HTTP는 원래 TCP와 직접 통신했지만 HTTPS는 HTTP-SSL-TCP를 거쳐 통신을 한다. HTTPS는 HTTP에 비해 CPU나 메모리 등 리소스를 더 요구하지만 하드웨어의 발달로 속도 저하가 거의 없어 모든 웹 페이지에서 HTTPS를 적용한다.

SSL은 상대를 확인하는 수단으로 증명서를 제공한다. 증명서는 신뢰 할 수 있는 제3자 기관에 의해 발행되어 서버나 클라이언트가 실재한다는 사실을 증명한다. 그러면서 통신 상대가 본인이 통신하는 서버임을 나타내고 이용자는 개인 정보 누설 등의 위험성이 줄어들게 된다. 웹 인증은 덤.

# 💭 웹 통신의 흐름

<aside>
💡 가정 : Chrome을 실행해 주소에 특정 URL값을 입력
</aside>

> In 브라우저

브라우저 내부 규칙에 따라 의미 조사 → 의미에 따라 HTTP Req를 만듬 → 만들어진 Msg를 웹 서버로 전송 (우리가 택배 회사를 통해 택배를 보내는 느낌.)

OS에 송신을 의뢰할 때는 ip주소로 메시지를 받을 상대를 지정해야 하는데, 이 과정에서 DNS서버를 조회해야 한다.

DNS : 도메인 네임 시스템(DNS)은 인터넷전화번호부다. 우리가 'google.com'같은 도메인 이름을 웹에 입력하는 경우 DNS는 해당 사이트의 올바른 IP 주소를 찾는 역할을 합니다.

> In 프로토콜 스택, LAN 어댑터

프로토콜 스택이 브라우저한테 메시지를 받음 → Msg를 패킷 속에 저장 → 수신처 주소 등의 제어정보 추가 → 패킷을 LAN 어댑터에 넘김 → LAN 어댑터는 다음 Hop의 MAC 주소를 붙인 프레임을 전기신호로 변환해 LAN 케이블에 송출.

Hop : 컴퓨터 네트워크에서 출발지와 목적지 사이에 위치한 경로의 한 부분

프로토콜 스택은 비서가 일을 처리해주는 것처럼 통신 중 오류가 발생했을 때, 제어 정보를 써서 고쳐 보내거나, 각종 상황을 조절하는 등의 역할을 해준다.

> In 허브, 스위치, 라우터

LAN 어댑터가 송신한 프레임은 스위칭 허브를 경유하여 인터넷 접속용 라우터에 도착 → 라우터는 패킷을 프로바이더(통신사)에게 전달 → 패킷은 인터넷 입구에 있는 통신 회선에 의해 통신사용 라우터를 거쳐 인터넷에 들어가고 목적지로 흘러감.

> In 방화벽, 캐시서버

패킷은 인터넷 핵심부를 통과하여 웹 서버측의 LAN 에 도착 → 방화벽이 패킷 검사 → 캐시서버가 출입허가를 검사. (굳이 서버까지 가지 않아도 되는 경우를 골라냄)

> In 웹서버

패킷이 웹 서버에 도착하면 웹 서버의 프로토콜 스택은 패킷을 추출하여 메시지를 복원하고 웹 서버 애플리케이션에 넘김 → 메시지를 받은 웹 서버 애플리케이션은 요청에 따른 데이터를 ACK에 넣어 클라이언트로 회송 → 왔던 방식대로 응답 메시지가 클라이언트에게 전달

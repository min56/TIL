# HTTPS

![03-3.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c3f686a-80ab-40a1-88e7-ed54740869a8/03-3.png)

**인터넷 주소를 암호화해 전송하는 보안접속 방식**

- 인터넷 상에서 정보를 암호화하는 SSL프로토콜을 이용하여 웹브라우저(클라이언트)와 서버가 데이터를 주고 받는 통신 규약
- http 메세지(text)를 암호화하는 것

<aside> 📌 **HTTP + 보안 기능 = HTTPS**

</aside>

### SSL, TLS

클라이언트/서버 응용 프로그램이 네트워크로 통신을 하는 과정에서 도청, 간섭, 위조를 방지하기 위해 설계도

- 암호화를 해서 최종단의 인증, 통신 기밀성을 유지

- TLS는 SSL을 업그레이드 버전이다.

- 공개키 암호화 방식을 사용한다.

  ![crypto_asymmetric_key_01.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cf2e6313-fb06-41a8-8b7a-0434a7e37a66/crypto_asymmetric_key_01.jpg)

공개키 암호화 방식 : 암호화, 복호화를 시킬 수 있는 서로 다른 키 2개가 존재한다. 이 두 개의 키는 서로 1번 키로 암호화하면 반드시 2번 키로만 복화화를 시킬 수 있고 2번 키로 암호화 하면 반드시 1번키로만 복호화가 가능하다는 규칙이 있다.

**공개키 암호화 방식 순서**

1. 하나의 키는 모두에게 공개하는 공개키로 만들어 공개키 저장소에 등록한다.
2. 서버는 서버만 알 수 있는 개인키를 소유하고 있는다.
3. 공개키로 암호화된 http 요청 → HTTPS 프로토콜을 사용한 요청이 온다.
4. 서버는 개인키를 이용해 암호화된 문장을 해석한다.
5. 요청에 맞는 응답을 다시 개인키로 암호화해 요청한 클라이언트에게 보내주게 된다.
6. 응답을 받은 클라이언트는 공개키를 이용해 암호화 된 HTTPS응답을 해독하고 사용한다.

**공개키 저장소**

누구나 공개키 저장소에서 공개키를 얻을 수 있기 때문에 보안상의 의미는 없지만 서버가 주는 데이터를 알 수 있다.

- 공개키로 해독이 가능했기 때문에 해당 서버로부터 온 응답임을 확신가능 하다.

**HTTPS도 완벽히 안전할 수 없다.**

HTTPS가 암호화 방식을 사용하기 때문에 HTTP보다 안전하지만 안전하지 않은 사이트를 들어가게 되면 HTTPS는 **“주의 요함”, “안전하지 않은 사이트” 처럼 알림**을 주게 됩니다.
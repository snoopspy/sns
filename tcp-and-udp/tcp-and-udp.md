TCP and UDP
===

## 준비
* https://gitlab.com/gilgil/scs.git repository를 clone 받아서 tc(tcp client), ts(tcp server), uc(udp client), us(udp server) 프로그램을 빌드한다.


## UDP 통신 테스트

* udp server를 실행한다.
```
./us 1234
```

* udp client를 실행하고 나서 "aaaaa", "bbbbb", "ccccc"를 순차적으로 보낸다.
```
./uc 127.0.0.1 1234
```

* 통신 과정에서 packet을 확인한다.


### TCP 통신 테스트
* tcp server를 실행한다.
```
./ts 1234
```

* tcp client를 실행하고 나서 "aaaaa", "bbbbb", "ccccc"를 순차적으로 보낸다.
```
./tc 127.0.0.1 1234
```

* 통신 과정에서 packet의 갯수를 확인한다.

* 송수신되는 packet의 SEQ number 및 ACK number 값을 확인한다.  
[tcp-seq-ack-test-blank.drawio](tcp-seq-ack-test-blank.drawio) / [tcp-seq-ack-test.drawio](tcp-seq-ack-test.drawio).

## UDP 통신 차단 테스트
* udp 통신을 차단한다(서버측).
```
sudo iptables -A INPUT -p udp --dport 1234 -j DROP
```

* "aaaaa"를 보낸다.

* udp 통신을 허용한다(서버측).
```
sudo iptables -D INPUT -p udp --dport 1234 -j DROP
```

* "bbbbb", "ccccc"를 보낸다.

* us측에서 데이터의 수신 여부와 packet을 확인한다.


## 존재하지 않는 host로 TCP connection 테스트
* 존재하지 않는 host로 tcp connection을 시도한다.
```
./tc 2.2.2.2 1234
```

* packet의 retransmission 패턴을 알아 본다.


## TCP 통신 차단 테스트
* tc와 ts의 connection을 맺어 놓는다.

* tcp 통신을 차단한다(서버측).
```
sudo iptables -A INPUT -p tcp --dport 1234 -j DROP
```

* "aaaaa", "bbbbb", ""ccccc""를 보낸다.

* tcp 통신을 허용한다(서버측).
```
sudo iptables -D INPUT -p tcp --dport 1234 -j DROP
```

* UDP와는 다르게 15바이트(aaaaabbbbbccccc)가 Application 레벨에서 모두 전송이 됨을 확인하고, data retransmission 패턴 및 송수신되는 packet의 SEQ number값을 확인한다.


## 결론
* TCP는 Data를 송수신하기 이전에 연결 과정을 거치며(connection oriented), UDP는 이러한 연결 과정이 없다(connectionless).

* TCP는 연결 과정에서 상대방의 SEQ number negotiation, RTT(Round-Trip Time) 계산 등 다양한 정보를 수집한다.

* TCP는 제대로 된 송수신의 보장을 위해 SEQ number 및 ACK number 필드를 사용한다.

* TCP의 ACK flag는 ACK number가 유효한지 아닌지를 의미하며, 클라이언트가 서버로 접속을 시도하는 제일 처음 packet을 제외하고는 모두 1의 값을 가진다.

* TCP의 SEQ number는 송신하는 Data의 크기만큼 증가하고, 특정 flag(SYN, FIN)에 대해 1(하나) 증가한다(RST flag에 대해서는 무시함).

* TCP의 SEQ, ACK number는 제 3자로부터의 packet injection attack을 방지하기 위하여 처음 값을 random으로 결정한다. 이러한 random SEQ number를 guessing하는 TCP sequence prediction attack 기법도 있다.

* UDP는 TCP에서 제공하는 이러한 retransmission 로직이 없다. 필요한 경우 Application에서 이러한 기능을 제공해야 한다.


## Youtube
* TCP와 UDP에 대한 설명(1) https://youtu.be/kG4uABh5EH4
* TCP와 UDP에 대한 설명(2) https://youtu.be/LBKdkZwmUnc
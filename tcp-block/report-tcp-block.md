### 과제
Out of path 환경에서 TCP Packet Injection(RST, FIN 플래그를 포함한)을 이용하여 사이트를 차단하는 프로그램을 작성하라.

### 실행
```
syntax : tcp-block <interface> <pattern>
sample : tcp-block wlan0 "Host: test.gilgil.net"
```

### 상세
* Out of path의 대표격인 pcap library를 이용하여 패킷을 수신한다.

* 수신된 패킷의 TCP Data 영역에 pattern이 검색되는 경우 차단 패킷을 양쪽으로 송신한다.

* 정방향(forward)은 RST flag를 포함한 패킷을 송신한다(자신의 머신에 wget이나 웹브라우저를 이용해서 테스트).

* 역방향(backward)는 FIN flag 및 "HTTP/1.0 302 Redirect\r\nLocation: http://warning.or.kr\r\n\r\n"의 TCP Data를 포함한 패킷을 송신한다. 자신에게 전송하는 역방향 패킷은 pcap을 이용하는 경우 Linux에서 작동하지 않을 수 있으므로 [raw socket](https://www.google.com/search?q=raw+socket+example&oq=raw+socket+example)를 이용하여 전송하도록 한다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

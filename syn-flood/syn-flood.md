SYN flood
===

https://gitlab.com/gilgil/scs.git git repository를 clone받아서 make 명령어로 빌드를 한다. bin 폴더에 tc, ts, uc, us 실행 파일이 생성된다. 다음과 같은 명령어로 간단한 tcp server(port 번호 1234)를 띄워 놓는다(Victim).
```
$ ./ts 1234
```

클라이언트에서 tc 명령어를 통해서 연결과 데이터 송신이 제대로 되는지 확인한다.
```
$ ./tc 127.0.0.1 1234
```

서버에서 다음과 같은 명령어로 syncookies 옵션 값을 확인한다. default는 1이며, 이 경우 외부로부터의 SYN flooding attack에 대한 방어 기능이 on되어 있다.
```
$ sysctl -a | grep syncookies
net.ipv4.tcp_syncookies = 1
```

victim 대상이 되는 호스트에서 tcp_syncookies 값을 0으로 하여 SYN flooding attack 방지 기능을 off로 만든다.
```
$ sudo sysctl -w net.ipv4.tcp_syncookies=0
```

hping3 명령어를 통해서 SYN packet을 하나만 보내 본다.
```
$ hping3 127.0.0.1 -p 1234 -S -c 1
```

서버에서 netstat 명령어로 SYN RECEIVED 상태의 소켓이 존재하는지 확인한다.
```
$ netstat -apn | grep :1234
```

서버에서 SYN_RECV 상태의 소켓이 존재하지 않는 것은 SYN, SYN+ACK 송수신에 의해 클라이언트가 RST packet(나는 1234와 관련되어 요청한 적이 없다)을 서버에게 전달하게 되고, 서버에서는 소켓의 상태가 SYN RECEIVED 상태에서 CLOSED 상태로 전환이 되기 때문이다. 따라서 적당한 방법을 사용하여 클라이언트에서 서버로 전달되는 RST packet을 차단하도록 한다.

이후 hping3 명령어를 통하여 SYN flooding attack을 하게 되면 하나의 패킷에 의해 서버에서 SYN RECEIVED 상태의 소켓이 계속 증가하는 것을 볼 수 있다. SYN RECEIVED 상태의 소켓이 계속 증가하다거 더 이상 외부로부터의 연결 요청을 받을 수 없게 된다(SYN packet에 대해 SYN+ACK packet으로 반응할 수 없다). 이 소켓의 갯수는 listen 함수의 인자 값(backlog)으로 결정이 된다. backlog 값을 변경하면서 테스트를 다시 해 본다.

SYN packet을 좀 더 주기적으로 보내게 한다. 몇 초만 지나면 서버는 더 이상 외부로부터의 접속을 어려워지게 된다. 반면 기존에 이미 연결되어 있는 소켓은 제대로 송수신이 잘 됨을 확인할 수 있다.
```
$ hping3 127.0.0.1 -p 1234 -S -i u100000
```

요즘 나오는 대부분의 OS는 이러한 SYN flooding attack에 대해 방어할 수 있는 메커니즘이 구현되어 있다. 다음 명령어를 통해서 syncookies 값을 다시 on시켜서 SYN flooding attack에 대해 방어할 수 있도록 한다.
```
$ sudo sysctl -w net.ipv4.tcp_syncookies=1
```

## Youtube
https://youtu.be/08ft80U4xac
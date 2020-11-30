TCP block
===

[malicious-site.pptx](malicious-site.pptx) 파일을 참고한다.

[tcp-block-diagram.drawio](tcp-block-diagram.drawio) 파일을 참고하여 차단 패킷을 전송하는 흐름을 파악한다.

## RST and FIN packet

* TCP 헤더에 RST flag가 set되는 경우 RST packet을 받은 호스트는 TCP 연결을 강제적으로 끊는다.

* TCP 헤더에 FIN flag가 set되는 경우 FIN packet을 받은 호스트는 Close Wait 상태가 된다. [구글링 참조](https://www.google.com/search?q=tcp+state+diagram)

* RST이건 FIN이건 상대방 호스트에 제대로 전달되면 established state가 아니기 때문에 더 이상 TCP Data의 송수신이 불가능하게 된다.

* FIN의 경우 TCP Data를 추가할 수 있고 의도하는 Data(HTML과 같은)를 전달할 수 있다.

## Forward and Backward

* 유해 패킷이 탐지되었을 때 같은 방향으로 송신되는 패킷을 Forward block packet, 반대 방향으로 송신되는 패킷을 Backward block packet이라고 한다. 유해 packet 탐지 및 차단 장비에서는 Forward와 Backward 방향으로 각각 RST 혹은 FIN 둘 중 하나를 선택하여 전송하게 된다.

* 국내의 경우 HTTP packet에 대해서는 Forward RST, Backward FIN을, HTTPS packet에 대해서는 Forward RST, Backward RST를 보내고 있다.

## Packet 생성 규칙

* org-packet : 캡쳐된 원래 패킷(유해 패킷)이라 명명한다.

* Ethernet header
  * smac : L2 switch의 CAM table이 깨지는 것을 방지하기 위해 자신 인터페이스의 mac 값을 사용한다.

  * dmac : Forward의 경우 org-packet의 ether.dmac, Backward의 경우 org-packet의 ether.smac 값을 사용한다.

* IP header
  * len : sizeof(IP) + sizeof(TCP) 값으로 설정하면 된다. FIN message가 존재하는 경우 메시지의 크기만큼 더해준다.

  * ttl : Forward의 경우 org-packet의 TTL 값을 사용하면 되고, Backward의 경우 적당한 TTL 값을 설정해 준다(일반적으로 128로 하면 무방).

  * sip, dip : Forward의 경우 org-packet의 값을 그대로 사용하면 되고, Backward의 경우 org-packet의 값을 바꿔서 설정한다.

* TCP header

  * sport, dport : Forward의 경우 org-packet의 값을 그대로 사용하면 되고, Backward의 경우 org-packet의 값을 바꿔서 설정한다.

  * seq : org-packet.seq 값에 org-packet.tcp_data_size 를 더한 값.

  * ack : org-packet.ack 값 그대로. Backward의 경우 seq와 ack 값을 바꾸어서 설정한다.

  * hlen : sizeof(TCP)

  * flag : RST flag나 FIN flasg를 set해 준다. SYN flag는 reset, ACK flag는 set해 준다.

* Checksum
  * Block packet을 송신하기 이전에 TCP header 및 IP header의 checksum 값을 제대로 설정해 준다.

## Checksum offload

* IPv4, TCP, UDP header에는 checksum이라는 field가 있다. 이러한 checksum 값 계산은 OS가 해주는데, 이러한 부하(load)를 경감(offload)해 주는 기능이 최신 OS에는 탑재되어 있다. Network adapter가 offload를 지원해주고, OS가 이를 인식하는 경우 checksum offload가 활성화되어 OS는 checksum 계산을 직접해 주지 않고 그냥 hardware로 packet을 넘겨 버린다. 이 경우 Wireshark로 packet을 잡으면 checksum이 잘못되었다고 나오지만, 실제 송신되는 packet에서의 checksum 계산은 adapter가 처리를 해서 제대로 된 checksum 값을 가진 packet이 송신된다.

* Wireshark에는 기본적으로 checksum validation 기능이 off되어 있어서 checksum이 맞는지 확인하는 로직이 비활성화되어 있다. 송신되는 packet의 checksum 값이 제대로 되어 있나 확인하기 위하여 Wireshark - Edit - Preferences - Protocols - IPv4에 가서 "Validate IPv4 summary in protocol tree" 기능을 enable시킨다. 똑같이 TCP 및 UDP에서도 checksum validation 기능을 enable한다. 참고로 IPv6에는 checksum field가 존재하지 않는다.

* OS 차원에서 checksum offload가 켜져 있는 상태에서 Wireshark로 packet을 잡으면 빨간 색의 packet이 너무 많이 보여 분석에 지장을 준다. 다음과 같은 명령어로 offload 기능을 비활성화시키는 것이 좋다.
```
sudo ethtool -K eth0 rx off tx off
```

## Youtube
https://youtu.be/5EOKiAN749w

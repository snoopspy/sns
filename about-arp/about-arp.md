About ARP
===

ARP 프로토콜에 대해서 이해를 한다. 본 실습은 공공 와이파이 환경에서 절대 하지 말고 별도의 공유기나 핫스팟 환경에서 테스트하도록 한다. 가상환경이라면 NAT mode가 아닌 Bridge mode로 변환을 해서 실습을 한다.

## 네트워크 정보 수집

* https://gitlab.com/gilgil/send-arp-test.git repository를 clone받는다.

* \<git\>/ppt 폴더 안에 있는 PPT 파일을 열어서 자신(me), 상대방(you), 게이트웨이(gateway)에 대한 mac과 ip 정보를 알아내어 적는다.

* linux는 'ifconfig', windows는 'ipconfig /all' 명령어로 네트워크 정보를 알아낼 수 있다.

* linux에서 gateway 정보는 'route -n' 명령어로로 알아낼 수 있다.

* android의 경우에는 'Network Info II'라는 앱을 설치하면 자신의 네트워크 정보를 알 수 있다. 필요에 따라 ICMP packet을 테스트할 수 있는 Ping 앱('Ping & Net')도 설치해 놓는다.


## PING packet 실습

* Wireshark를 실행하여 'ping 8.8.8.8' 명령어에 의한 ICMP packet(icmp.pcap으로 저장)을 잡아 ppt 파일의 ICMP 란에 ETH 헤더와 IP 헤더에 mac과 ip 정보를 입력한다.

## ARP packet 실습

* 'sudo arp -d \<gateway\>'라는 명령어로 자신의 ARP cache table을 삭제하게 되면 외부와의 통신을 위해서 자신의 호스트와 gatway 사이에 ARP packet(ARP request, ARP reply)가 발생한다. 이 상태에서 잡힌 ARP packet(arp.pcap으로 저장)을 보면서 PPT 파일의 ARP 란에 mac과 ip 정보를 입력한다.

## 프로그램을 이용하여 ARP request packet 전송

* \<git\>/src 에 있는 send-arp-test.pro 프로젝트를 Qt Creator에서 열어서 빌드를 하고 실행을 해 본다. Wireshark에서 관련된 ARP packet이 잡히는 것을 확인할 수 있다.

* main.cpp 코드 내부에 있는 값들을 수정하여 ARP request packet을 발생시켜 실제 gateway로부터 ARP reply가 올 수 있도록 실습을 해 본다(저장한 arp.pcap 파일 내부에서 보이는 ARP packet과 동일한 ARP packet을 발생시키면 된다).

## 프로그램을 이용하여 상대방 컴퓨터의 ARP cache table 감염(infection)

* main.cpp 코드 내부에 있는 값들을 적당히 수정하여 상대방 컴퓨터(victim)에서 gateway에 대한 ARP cache table을 감염시켜 본다.

* 이 경우(attack이 성공한 경우) 상대방 컴퓨터에서 ARP cache table이 변경되고, 외부 ping을 때렸을 때 그 ping packet이 자신(attacker)에게 오게 되며, 상대방 컴퓨터에서는 정상적인 IP 통신을 할 수 없게 된다(인터넷이 막히는 것처럼 된다).

## Youtube
About ARP(1) : https://youtu.be/kAUGd9xtUHE

About ARP(2) : https://youtu.be/4Ia6Q-MXVzY

About ARP(3) : https://youtu.be/__p4yCeYI0k

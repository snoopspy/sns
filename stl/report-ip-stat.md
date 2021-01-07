### 과제
pcap file로부터 packet을 읽어서 IP별 송신 패킷 갯수, 수신 패킷 갯수, 송신 패킷 바이트, 수신 패킷 바이트를 출력하는 프로그램을 작성하라.

### 실행
```
syntax : ip-stat <pcap file>
sample : ip-stat test.pcap
```

### 상세
* pcap_open_live 함수를 사용하지 않고 [pcap_open_offline](https://linux.die.net/man/3/pcap_open_offline) 함수를 사용하면 실제 NIC이 아닌 [pcap 파일]로부터 패킷을 읽을 수 있다.

* Wireshark - Statistics - Endpoints - IPv4 참고할 것.

* 가능하다면 IPv4 뿐만 아니라 Ethernet, TCP, UDP등에 대한 Endpoint 정보도 출력해 볼 것.

* sample pcap file : [test.pcap](test.pcap)

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

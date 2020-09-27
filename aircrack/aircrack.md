Aircrack
===

WPA(2) 환경에서 Station이 AP에 접속을 할 때 발생하는 eapol 및 최소 하나만의 beacon frame이 있으면 brute-force attack 기반으로 해당 AP의 비밀번호를 알아낼 수 있다.

## 실습
* AP의 정보
  * SSID : gilgil-ap
  * 비밀번호 : "gilgil-is-handsome-000000" 에서부터 "gilgil-is-handsome-9999999" 까지 중의 하나.

* [pcap file](gilgil-ap-beacon-eapol1234)
  * AP가 전송하는 beacon frame 하나와 Station이 AP에 접속할 때 발생한 eapol 패킷이 들어가 있음.

* 이 상황에서 wordlist를 스스로 만들어([create-dictionary.cpp](create-dictionary.cpp)) AP의 비밀번호를 알아내어라. list가 1백만 개정도일 때 대략 어느 정도 시간이 소요되는지를 파악하도록 한다.

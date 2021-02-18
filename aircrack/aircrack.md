* WPA(2) 환경에서 Station이 AP에 접속을 할 때 발생하는 eapol(ANonce, SNonce) 및 최소 하나만의 beacon frame이 있으면 brute-force attack 기반으로 해당 AP의 비밀번호를 알아낼 수 있다.

* ANonce는 eapol 1, 3 패킷에 존재하고 SNonce는 eapol 2 패킷에 존재한다. 그러므로 eapol는 1이나 3 패킷 둘 중 하나가 포함되어야 하며, 동시에 eapol 2 패킷도 존재해야 한다.

## 실습
* 공유기(SSID : gilgil-ap)의 비밀번호를 알아 내어라. 비밀번호는 "gilgil-is-handsome-000000" 에서부터 "gilgil-is-handsome-9999999" 까지 중의 하나이다.

* 해당 공유기에 Deauth Attack을 하여 최초 하나의 Station으로부터의 재연결을 시도하는 과정을 pcap file로 저장한다.

* 해당 pcap file[(gilgil-ap-beacon-eapol1234.pcap)](gilgil-ap-beacon-eapol1234.pcap)에는 AP가 전송하는 beacon frame 하나와 Station이 AP에 접속할 때 발생한 eapol 패킷이 들어가 있다.

* wordlist를 스스로 [만들어](create-dictionary.cpp) wordlist.txt 파일을 생성한다.

* 다음과 같은 명령어로 공유기의 비밀번호를 알아낼 수 있다. wordlist가 1백만 개정도일 때 대략 어느 정도 시간이 소요되는지를 파악하도록 한다.

```
aircrack-ng aircrack-ng gilgil-ap-beacon-eapol1234.pcap -w wordlist.txt 
```

* GPU가 달린 머신이라면 hashcat이라는 툴을 이용하여 좀 더 빠르게 Dictionary attack, Brute-Force attack, Rule-based attack을 실행할 수 있다.  
[https://hashcat.net/wiki/doku.php?id=cracking_wpawpa2](https://hashcat.net/wiki/doku.php?id=cracking_wpawpa2)


## References
https://github.com/wifihack/doc
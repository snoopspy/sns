### 과제
arp spoofing 프로그램을 구현하라.

### 실행
```
syntax : arp-spoof <interface> <sender ip 1> <target ip 1> [<sender ip 2> <target ip 2>...]
sample : arp-spoof wlan0 192.168.10.2 192.168.10.1 192.168.10.1 192.168.10.2
```

### 상세
* 이전 과제(send-arp)를 다 수행하고 나서 이번 과제를 할 것.

* "arp-spoofing.ppt"의 내용을 숙지할 것.

* 코드에 victim, gateway라는 용어를 사용하지 말고 sender, target(혹은 receiver)라는 단어를 사용할 것.

* sender에서 보내는 spoofed IP packet을 attacker가 수신하면 이를 relay하는 것 코드를 구현할 것.

* sender에서 infect가 풀리는(recover가 되는) 시점을 정확히 파악하여 재감염시키는 코드를 구현할 것.

* (sender, target) flow를 여러개 처리할 수 있도록 코드를 구현할 것.

* 가능하다면 주기적으로 ARP infect packet을 송신하는 기능도 구현해 볼 것.

* attacker, sender, target은 물리적으로 다른 머신이어야 함. 가상환경에서 Guest OS가 attacker, Host OS가 sender가 되거나 하면 안됨.

* Vmware에서 Guest OS를 attacker로 사용할 때 sender로부터의 spoofed IP packet이 보이지 않을 경우 [vmware_adapter_setting](vmware_adapter_setting.pdf) 문서를 참고할 것.

* Host OS의 네트워크를 사용하지 않고 별도의 USB 기반 네트워크 어댑터를 Guest OS에서 사용하는 것을 추천. 다이소에서 5000원으로 구매할 수 있음. - [https://www.youtube.com/watch?v=f8baVYPM9Pc](https://www.youtube.com/watch?v=f8baVYPM9Pc)


### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

* 절대 공공 와이파이 네트워크를 대상으로 테스트하지 말고 핫스팟과 같은 소규모 네트워크를 구성하여 테스트할 것.

* 본 과제는 어려운 레벨에 속하므로 충분한 시간을 투자하여 구현할 것(마감 하루 이틀 전에 과제 시작하지 말고).

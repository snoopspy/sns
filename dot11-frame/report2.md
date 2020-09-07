### 과제
Beacon Flooding Attack 프로그램을 제작하라.

### 실행
```
syntax : beacon-flood <interface> <ssid-list-file>
sample : beacon-flood mon0 ssid-list.txt
```

### 상세
* [libtins](http://libtins.github.io/)를 설치하고 예제를 직접 따라해 보면서 사용 방법을 익힌다.

* [Beacon Flooding Attack](https://gilgil.gitlab.io/2020/09/07/2.html) 예제를 빌드하고 실행해 본다.

* libtins를 사용하지 않고 직접 Beacon frame(Radiotap Header + IEEE 802.11 Beacon frame + IEEE 802.11 Wireless Management)을 만들어 하여 전송하는 프로그램을 제작한다.

* Beacon frame을 직접 만들기 어려울 경우 기존의 실제 Beacon frame을 pcap으로 잡아서 거기에 SSID 값만 바꾸어서 전송해 보도록 한다.

* ssid-list.txt 에 포함된 SSID 갯수는 최소 10개 이상이 되도록 한다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

### 과제
특정 WiFi Device의 신호 세기를 출력하는 프로그램을 제작하라.

### 실행
```
syntax : signal-strength <interface> <mac>
sample : signal-strength mon0 00:11:22:33:44:55
```

### 상세
* [https://www.radiotap.org](https://www.radiotap.org) 사이트의 defined fields, suggest fields, rejected fields 등을 숙지하고 Alignment in Radiotap 이라는 개념도 이해한다.

* 802.11 frame은 대부분 addr1, addr, addr3 정보가 들어가 있다. 여기에서 ta 정보를 추출하고 radiotap header에서 signal strength를 알아내어 그 크기를 숫자로 출력하도록 한다.

* [https://gitlab.com/gilgil/g/tree/master/bin/pcap/dot11](https://gitlab.com/gilgil/g/tree/master/bin/pcap/dot11) URL 에 샘플 802.11 pcap file이 있으니 이를 이용하여 디버깅(출력하는 정보가 제대로 맞는지를 Wireshark에서 보여주는 결과와 비교하면서 확인)을 한다.

* 가능하다면 Chart와 같은 컴포넌트를 이용하여 GUI 형식으로도 보여줄 수 있도록 한다( [https://doc.qt.io/qt-5/qtcharts-linechart-example.html](https://doc.qt.io/qt-5/qtcharts-linechart-example.html) ).

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

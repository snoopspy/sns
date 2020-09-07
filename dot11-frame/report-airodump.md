### 과제
airodump-ng와 비슷한 출력을 할 수 있는 프로그램을 작성하라.

### 실행
```
syntax : airodump <interface>
sample : airodump mon0
```

### 상세
* Beacon Frame에서 BSSID, Beacons, (#Data), (ENC), ESSID는 필수적으로 출력한다(괄호 항목은 선택).

* Beacon Frame에서 PWR 정보는 Radiotap Header에 있으며, Radiotap Header 분석은 [Radiotap](https://www.radiotap.org) 사이트를 참고한다.

* Station은 기본적으로 AP와 연결되어 통신을 하지만 그렇지 않은 Frame(Probe Request)도 존재한다.

* 가능하다면 Channel Hopping 기능을 추가한다.

* [가상의 무선 네트워크 어댑터를 생성](https://gilgil.gitlab.io/2020/09/07/1.html) 기법을 이용하여 디버깅을 편하게 할 수도 있다.

* 필요한 경우 GitHub에 있는 [airodump-ng](https://github.com/aircrack-ng/aircrack-ng/tree/master/src/airodump-ng) 소스 코드를 참조한다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

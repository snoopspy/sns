### 과제
Channel hopping을 하면서 Beacon frame을 수신할 경우 Deauth Attack을 하는 프로그램을 작성하라.

### 실행
```
syntax : wifi-jammer <interface>
sample : wifi-jammer mon0
```

### 상세
* "wireless-tools"로 검색을 하여 [wireless_tools.29.tar.gz](https://hewlettpackard.github.io/wireless-tools/wireless_tools.29.tar.gz) 파일을 다운받는다.

* 압축을 풀고 iwlib.h 및 iwlib.c 파일을 이용하여 channel list와 channel hopping하는 로직을 구해 온다.

* 프로그램이 시작되면 channel list를 구해 와서(iwlist 명령어를 이용해도 되고 iwlib 모듈을 이용해도 되고) 일정한 주기(120 msec, 250 msec, 1 sec)로 channel hopping을 한다(iwconfig 명령어를 이용해도 되고 iwlib 모듈을 이용해도 되고).

* Beacon frame이 캡쳐되면 실시간으로 Deauth frame을 만들어서 broadcast로 전송한다.

* Station에서 ping을 때려 놓은 상태에서 연결이 제대로 끊기는지 확인한다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

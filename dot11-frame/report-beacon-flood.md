### 과제
Beacon Flooding Attack 프로그램을 제작하라.

### 실행
```
syntax : beacon-flood <interface> <ssid-list-file>
sample : beacon-flood mon0 ssid-list.txt
```

### 상세

* [libtins](http://libtins.github.io/)를 설치하고 예제를 직접 따라해 보면서 사용 방법을 익힌다.
```
sudo apt install cmake libtest-dev libssl-dev
git clone https://github.com/mfontanini/libtins.git
cd libtins
git tag
git checkout <latest tag>
mkdir build
cd build
cmake ..
make -j$(NPROC)
sudo make install
sudo cp /usr/local/lib/libtins* /usr/lib
```

* [Beacon Flooding Attack](https://gilgil.gitlab.io/2020/09/07/2.html) 예제를 빌드하고 실행해 본다(예전 스마트폰에서는 SSID List가 보이지만 요즘 스마트폰에서는 보이지 않는 현상이 있다).

* libtins를 사용하지 않고 직접 Beacon frame(Radiotap Header + IEEE 802.11 Beacon frame + IEEE 802.11 Wireless Management)을 만들어 하여 전송하는 프로그램을 제작하는 것을 추천.

* Beacon frame을 직접 만들기 어려울 경우 기존의 실제 Beacon frame을 pcap으로 잡아서 거기에 SSID 값만 바꾸어서 전송해 보도록 한다.

* ssid-list.txt 에 포함된 SSID는 일단 영어로 작성하고 다음에 한글로 테스트해 본다. 그리고 SSID 갯수를 하나만 설정하여 제대로 작동하는지 확인하고, 확인이 된 이후에는 10개까지 넣어서 작동하는지 확인한다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

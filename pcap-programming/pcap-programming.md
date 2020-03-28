Pcap programming
===

Wireshark에서 잡힌 packet을 이제 programming을 통해서 실습해 보도록 한다.

pcap_t라는 핸들을 이용하여 packet을 수집(capture) 및 전송(send)를 raw level로 할 수 있다. 일부 OS에 따라서 관리자(root) 권한이 필요하기도 하니, 실행할 때에는 가급적 root 계정으로 실행한다.

|Description| Functions|
|---|---|
|pcap 핸들 열기|pcap_open, pcap_open_live, pcap_open_offline|
|pcap 핸들 닫기|pcap_close|
|packet 수신|pcap_next_ex|
|packet 송신|pcap_sendpacket|

그 외에도 다양한 API가 있으니 구글링을 통하여 pcap API를 숙지하시기 바랍니다.

## Linux
* libpcap을 설치해야 한다. pcap.h 파일을 include하고 링크 과정에서 '-lpcap' 옵션을 추가한다. 일후 pcap function은 관리자 권한을 요구하니 root로 실행하도록 한다.

   ```
   $ sudo apt install libpcap-dev
   ```

* http://www.tcpdump.org/pcap.html 에 있는 내용을 숙지한다.

* 간단한 버전으로 실습해 본다( [pcap-test.zip](pcap-test.zip) ).

## Windows
* WinPcap( https://www.winpcap.org )이나 npcap( https://npcap.org or https://nmap.org/npcap )을 설치하여 빌드 환경을 구축한다.

* www.winpcap.org > Documentation > "The WinPcap manual and tutorial for WinPcap 4.1.2" 에 있는 "WinPcap tutorial: a step by step guide to using WinPcap"의 9가지 예제를 그대로 따라해 본다.

* wincap.org 사이트에 있는 소스 코드는 간혹 빌드가 되지 않는 경우가 있다. [winpcap-sample.zip](winpcap-sample.zip) 파일을 만들어 놓았으니 참고한다.

## Youtube
[https://youtu.be/moPv28MWSas](https://youtu.be/moPv28MWSas)

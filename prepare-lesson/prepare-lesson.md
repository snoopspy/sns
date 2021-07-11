Prepare lesson
===

강의 실습의 진행은 Linux와 Windows OS를 중심으로 이루어 집니다. 따라서 다음과 같은 환경을 세팅해 주시기 바랍니다.

* Linux 설치 ([Kali(권장)](https://www.kali.org/) 혹은 [Ubuntu](https://www.ubuntu.com/))  
Host OS에 설치해도 되나 대부분의 교육생이 Windows, macOS를 사용하는 관계로 virtual(vmware or virtualbox) 환경에서 Guest OS로 Linux를 설치해 주시기 바랍니다(Memory는 4GB 이상 확보할 것 / CPU는 Host OS 갯수만큼 할당). Memory가 제한된 경우에는 USB로 multi booting할 수 있도록 준비해 놓으시기 바랍니다.
https://github.com/snoopspy/cpu-test tool을 가지고 CPU의 할당에 제대로 되어 있나 확인을 해 봅니다.

* Wireshark 설치 ([wireshark.org](https://www.wireshark.org/))  
"sudo apt install wireshark" 명령어로 설치할 수 있습니다. Windows에서는 wireshark.org 사이트에 가서 설치하시면 됩니다(WinPcaP과 npcap이 중복되어 설치되지 않도록 할 것). 네트워크 패킷을 잡는 일이 많으니까 Host OS 및 Guest OS 두군데 다 설치해 놓으시기 바랍니다.

~~* SnoopSpy 설치 ([snoopspy.com](http://snoopspy.com/))  
아직 Windows용 밖에 없습니다. 수업 시간에 종종 사용하는 일이 있으니 미리 설치해 두세요. [WinPcap과 Npcap 설치 문제 해결](https://gilgil.gitlab.io/2019/07/25/1.html) 문서를 참고하시기 바랍니다.~~

* Windows에서 불필요한 어댑터 삭제  
Windows에서 "ipconfig" 명령어를 실행하면 불필요한 어댑터들이 많이 나옵니다. 다음과 같응 명령어를 통해서 정리를 해 줍니다(관리자 권한으로 실행해야 함).
  ```
  netsh interface isatap set state disabled
  netsh interface teredo set state disabled
  netsh in 6to4 set state disable
  ```

* Windows에서 LoopBack Adapter 설치  
linux의 dummy interface와 비슷한 역할을 합니다.
  ```
  Windows > Run > "hdwwiz" > Next >
  Install the hardware that I manually select from a list (Advanced) >
  Network Adapters > Microsoft > Microsoft KM-TEST loopback Adapter >
  Next > Next > Finish" 로 설치.  
  Windows > "Change adapter settings" > 새로 설치된 어댑터 이름은 "dum0"로 변경 >
  오른쪽 클릭 > Properties > 모든 item들을 disable 시킬 것 >
  재부팅하여 wireshark에서 해당 어댑터가 보이는지 확인.
  ```
* g++ 설치  
  Linux에서 "sudo apt install g++" 명령어를 통하여 C++ 컴파일러를 설치합니다.

* Qt 설치 ([qt.io](http://qt.io))  
C/C++ 개발 IDE로 QtCreator라는 것이 있는데, Linux에서 C/C++을 많이 해 본 사람은 굳이 설치할 필요가 없습니다. apt(Advanced Package Tool)로 설치하지 말고 https://qt.io > Download. Try. Buy. > Go open source > Download the Qt Online Installer로 설치를 하시기 바랍니다.

  전부 설치할 필요는 없고 Qt 5.X.X 최선 버전의 Desktop gcc 64-bit와 Qt Creator만 설치해도 됩니다. online installer로 설치를 할 수도 있고 offline 설치 파일을 다운받아서 설치를 할 수도 있습니다. [qt archive](http://download.qt.io/archive/qt/)  

  /usr/lib/x86_64-linux-gnu/qtchooser/default.conf 파일을 생성하여 다음과 같은 항목을 추가하여 command line에서도 qmake가 실행이 될 수 있도록 합니다(5.14.2 라고 되어 있는 숫자는 자신의 머신에 설치된 qt의 버전에 맞게 수정 요망).
  ```
  /opt/Qt/5.14.2/gcc_64/bin
  /opt/Qt/5.14.2/gcc_64/lib
  ```

* [github.com](https://github.com/) 혹은 [gitlab.com](https://gitlab.com/) 사이트 회원 가입  
git 서비스를 하는 곳 중에 가장 유명한 사이트들이니 회원 가입을 해 주시기 바랍니다.

* git 설치  
Linux는 "sudo apt install git", Windows는 [git-scm.com](https://git-scm.com/) 사이트에서 다운받아 설치할 수 있습니다.




## Youtube
https://youtu.be/pb9cPU_vt5Y
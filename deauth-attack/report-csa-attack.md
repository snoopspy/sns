### 과제
CSA Attack 프로그램을 작성하라.

### 실행
```
syntax : csa-attack <interface> <ap mac> [<station mac>]
sample : csa-attack mon0 00:11:22:33:44:55 66:77:88:99:AA:BB
```

### 상세
* 기존 beacon frame을 capture한 이후 tagged parameter에 5바이트의 Channel Switch Announcement 정보를 삽입하여 전송한다. New Channel Number는 실제 채널 값이 아닌 임의의 번호. 가급적 tag number가 정렬되도록 할 것.

|Field|Value(hexa decimal)|
|---|---|
|Tag Number(CSA)|37(25)|
|Tag Length|3(03)|
|Channel Switch Mode|1(01)|
|New Channel Number|13(0D)|
|Channel Switch Count|3(03)|

* capture된 beacon frame에 FCS(Frame checksum) 정보가 있을 경우에 이 4바이트는 무시해야 한다.

* \<ap mac\>만 명시되는 경우에는 AP broadcast frame을 발생시킨다.

* \<station mac\>까지 명시되는 경우에는 AP unicast frame을 발생시킨다.

* 너무 많은 패킷을 발생시키면 무선 네트워크 사용에 지장을 줄 수 있으므로 적당히 sleep을 넣어 준다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

## Youtube

* CSA(Channel Switch Announcement) Attack : https://youtu.be/XTJ_GA7xI7w?si=Qsec_QiQ-M_F78g6
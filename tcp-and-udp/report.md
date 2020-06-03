### 과제
echoclient, echoserver 프로그램을 제작하라.

### 실행
```
echoclient:
syntax : echoclient <ip> <port>
sample : echoclient 192.168.10.2 1234

echoserver:
syntax : echoserver <port> [-b]
sample : echoserver 1234 -b
```

### 상세
* echoclient(이하 client)는 echoserver(server)에 TCP 접속을 한다.

* client는 사용자로부터 메세지를 입력받아 server에 메세지를 전달한다.

* server는 받은 메세지를 화면에 출력하고 client에게 그대로 보낸다.

* server는 -b(broadcast) 옵션이 주어진 경우 접속되어 있는 모든 client에게 메세지를 보낸다.

* client는 server로부터 메세지를 받으면 화면에 출력한다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

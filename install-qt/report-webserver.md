### 과제
간단한 웹서버 프로그램을 작성하라.

### 실행
```
webclient
```

### 상세
* Qt Creator > File > New File or Project > Application > Qt Widgets Application을 선택한다.

* Base class는 QMainWidow가 아닌 QWidget으로 하여 프로젝트를 생성한다.

* 화면을 구성하고 TCP 및 SSL 통신을 할 수 있는 코드를 작성한다.

* SSL 여부를 선택할 수 있는 기능을 추가하여 그 여부에 따라 TCP(HTTP) 혹은 SSL(HTTPS) 통신이 되도록 한다.

* 서버의 isListening() 함수를 이용하여 각 버튼 등의 활성화 여부를 설정할 수 있도록 한다.

* 가능하다면 화면의 좌표, LineEdit 및 PlainTextEdit의 내용을 파일로 입출력하여 마지막 값이 유지될 수 있도록 한다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(*.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

## Youtube
Web Client example using Qt : https://youtu.be/cKfQzEyedEw

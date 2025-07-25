### 과제
백만 개의 유해 사이트를 차단하라.

### 실행
```
syntax : 1m-block <site list file>
sample : 1m-block top-1m.txt
```

### 상세
* 이전 과제(netfilter-test)를 수행하고 나서 본 과제를 수행하도록 한다.

* zip 파일내의 1백만 개 사이트들을 유해사이트라고 간주하고 HTTP Reqeust에서 "Host: " 뒤의 Host 값을 알아 내서 백만 개 리스트 안에 존재하는지 판별하는 로직을 구현한다.

* 백만 개(정확하게 762564)의 사이트 리스트는 다음 파일을 참고한다. https://gitlab.com/gilgil/top-1m
<strike>http://s3.amazonaws.com/alexa-static/top-1m.csv.zip</strike>

* 로직의 구현은 메모리 및 검색 속도에 중점을 주도록 한다(프로그램을 돌려 놓고 실제로 인터넷 서핑 속도가 체감될 정도로 느려지면 안됨. 방법은 여러가지가 있을 수 있는데, 가장 쉽게할 수 있는 것이 sequential search이겠지만 이는 백만 개를 순차적으로 비교하는 로직이라서 검색 속도가 느려지게 됨. 어떠한 방법을 사용하든지 속도를 개선해 보고 가능하다면 메모리의 사용도 줄일 수 있는 다양한 방법을 고민해 볼 것).

* 백만 개를 메모리에 올릴 경우 시간이 얼마나 걸리는지(time diffing) 또한 메모리를 얼마나 많이 차지하는지 측정한다(top 명령어를 이용하여). 또한 백만 개에서 특정 호스트를 검색하는 부분에 대해서도 시간을 측정한다(time diffing).

* 웹브라우저로 테스트를 하게 되면 요즘 대부분의 사이트가 기본으로 HTTPS 통신을 하므로 제대로 된 테스트를 하기 힘들다. 따라서 wget 명령어를 통해서 HTTP 트래픽을 발생시켜 테스트해 보도록 한다.

* top-1m 파일 포맷은 본인 프로그램에 맞게 수정을 해도 무방하다.

### 기타
* git에는 소스 코드(h, c, cpp)만 올리지 말고 프로젝트 파일(Makefile 혹은 *.pro)도 같이 올릴 것.

* 메일에는 코드 파일을 첨부하지 말고 git 주소만 알려줄 것.

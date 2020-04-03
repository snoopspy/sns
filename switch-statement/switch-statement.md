switch statement
===

## switch statement에 대한 실행
* case에 있는 값들을 이용하여 jump table(branch table)을 만들어 O(1)으로 처리한다.

* case에 있는 값들이 sparse한 경우 binary search 방식을 사용한다.

* 이는 컴파일러 최적화에 따라 다르나, 최신 컴파일러는 대부분 이러한 방식을 사용한다.

[switch-statement-test.tar.gz](switch-statement-test.tar.gz)  

## Youtube
https://youtu.be/zwlR6FHRKvU

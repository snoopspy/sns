Byte order
===

## 십진수(decimal), 이진수(binary), 그리고 16진수(hexadecimal)

인간은 손가락이 10개이기 때문에 기본적으로 십진수를 사용한다. 컴퓨터 science는 2진수를 기반으로 한다.

참고 : [https://en.wikipedia.org/wiki/Arecibo_message](https://en.wikipedia.org/wiki/Arecibo_message)


## 10진수 / 16진수 / 2진수 정리
| decimal | hexadecimal | binary |
|---|---|---|
|0|0|0000|
|1|1|0001|
|2|2|0010|
|3|3|0011|
|4|4|0100|
|5|5|0101|
|6|6|0110|
|7|7|0111|
|8|8|1000|
|9|9|1001|
|10|A|1010|
|11|B|1011|
|12|C|1100|
|13|D|1101|
|14|E|1110|
|15|F|1111|

## Unit
| unit | description | range |
|---|---|---|
| nibble | byte의 절반의 의미로 4bit | 16가지 경우의 수를 가진다(0 ~ 15, 0x0 ~ 0xF) |
| byte | memory addressing 단위로 전통적으로 8bit | 256가지의 경우의 수를 가진다(0 ~ 255, 0x00 ~ 0xFF) |

* <b>hexidecimal 1자리 숫자로 nibble을 표현하고 2자리 숫자로 byte를 표현할 수 있다.</b>

## Practice
* http://gilgil.net:4660 에 접속하는 과정을 Wireshark에서 패킷을 잡으면 TCP Header에서 4660이라는 숫자가 보인다. 이는 Packet Bytes Window에서 보면 0x1234로 잡힌다. 이를 network byte order(이하 NBO)라고 한다.

* 코드 레벨에서는 4660이라는 숫자가 little endian인 경우 메모리에서 0x3412로 처리가 되고, big endian인 경우 메모리에서 0x1234로 처리가 된다. 이를 host byte order(이하 HBO)라고 한다.

* 코드 레벨에서 이러한 NBO와 HBO와의 변환을 해서 사용할 수 있어야 한다.

```cpp
#include <stddef.h> // for size_t
#include <stdint.h> // for uint8_t
#include <stdio.h> // for printf

void dump(void* p, size_t n) {
	uint8_t* u8 = static_cast<uint8_t*>(p);
	size_t i = 0;
	while (true) {
		printf("%02X ", *u8++);
		if (++i >= n) break;
		if (i % 8 == 0) printf(" ");
		if (i % 16 == 0) printf("\n");
	}
	printf("\n");
}
```
[byte-order-test.zip](byte-order-test.zip)

## Byte order
* NBO(network byte order) : 네트워크 레벨에서 숫자를 표현하는 순서

* HBO(host byte order) : 호스트에 레벨에서 숫자를 표현하는 순서

## Endian
* LE(little-endian) : HBO와 NBO가 다름

* BE(big-endian) : HBO와 NBO가 같음

## Conclusion
* Intel CPU의 경우는 대부분 LE 계열이고, ARM CPU의 경우에는 종류에 따라 BE, LE 계열로 구분되어 지기도 한다. 올바른 네트워크 프로그래밍을 하기 위해서는 LE 및 BE의 차이 및 NBO와 HBO간 변환를 시켜 주는 작동 원리를 이해하고 있어야 한다.

* <b>#include <netinet/in.h></b> 하면 아래와 같은 함수들을 사용할 수 있다. 아래 함수들은 자신의 CPU가 LE이던지 BE이던지 상관없이 작동할 수 있도록 컴파일러가 자신의 byte order를 알고 처리해 준다.  

| function | size | conversion |
|---|---|---|
| uint16_t <B>ntohs</B>(uint16_t netshort); | 2 byte | NBO to HBO |
| uint16_t <B>htons</B>(uint16_t hostshort); | 2 byte | HBO to NBO |
| uint32_t <B>ntohl</B>(uint32_t netlong); | 4 byte | NBO to HBO |
| uint32_t <B>htonl</B>(uint32_t hostlong); | 4 byte | HBO to NBO |

## References
[https://en.wikipedia.org/wiki/Endianness](https://en.wikipedia.org/wiki/Endianness)

## Youtube
https://youtu.be/VX1zPo1r0SY
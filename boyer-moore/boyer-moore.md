Boyer-Moore
===


## BM(Boyer-Moore) search algorithm의 특징
* strnstr 함수와 비슷한 역할을 한다.
```
char *strnstr(const char *big, const char *little, size_t len);
```

* 오른쪽에서 왼쪽으로 검색을 한다.

* Patten을 가지고 BC(Bad Chracter)table, GS(Good Suffix) table을 생성한다.

* 이후 Text가 들어왔을 때 검색 과정에서 mismatch가 났을 경우 index를 하나만 증가시키는 것이 아니라 BC table과 GS table 중 max 값을 이용하여 index를 증가시킨다.


## Pattern 작성 팁
* Pattern은 길면 길수록 좋다(BC 및 GS table 내부에 있는 shift 값이 늘어난다).

* Pattern에서 중복된 character가 많지 않도록 하는 것이 좋다.


## Code Download
https://gitlab.com/gilgil/boyer-moore-test


## Youtube
https://youtu.be/4s1noUxykk0

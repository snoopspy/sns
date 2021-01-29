### WiFi Scan의 종류
Station이 AP에 접속하기 위해서는 scan을 해야 한다. scan에는 2가지 종류가 있다.

1. Passive scan : AP는 주기적으로(1024 microseconds) 자신이 있음을 알리는 Beacon frame을 broadcast한다. 처음 가 보는 곳에 장소라 하더라도 WiFi list에서 해당 AP의 정보를 알 수 있는 것이 바로 Beacon frame 때문이다.

2. Active scan : Station은 "이러한 SSID를 가진 AP가 있나요?"라고 질의를 하게 되고(Probe Request), 해당 SSID를 가지고 있는 AP는 응답(Probe Response)을 해야 한다. Probe Response를 받은 Station은 해당 AP에 접속을 시도하게 된다.

### Hidden SSID
AP가 Beacon frame을 전송할 때 tagged parameter에 SSID를 포함하게 되는데, Hidden SSID 기능이 활성화되어 있으면 Beacon frame에 SSID가 포함되지 않는다. 따라서 외부에서는 해당 SSID를 가지는 AP의 존재 여부를 쉽게 알기가 어렵기 때문에 보안이 향상되어진다고 알려져 있다.  

하지만 Active scan 과정(Probe Request 및 Probe Response)의 패킷을 Attacker가 획득하면 쉽게 SSID 정보를 알아낼 수 있다.
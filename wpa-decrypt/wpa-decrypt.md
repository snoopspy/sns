Open mode에서는 송수신되는 Data frame이 암호화되지 않고 송수신된다. 반면에 WPA(2) mode에서는 송수신되는 Data frame이 PTK(Pairwise Transient Key)라는 것에 의해서 암호화되어 송수신된다.

|Mode|QoS Data frame|
|-|-|
|Open Mode|Radiotap Header + Qos Data Header + LLC + PlainText  |
|WPA(2) Mode|Radiotap Header + Qos Data Header + LLC + CipherText encrypted with PTK|

PTK는 다음과 같은 요소로 결정이 된다([https://github.com/wifihack/doc](https://github.com/wifihack/doc)).

```
PTK = f(SSID, Password, AP Mac, STA Mac, ANonce, SNonce)
```

SSID는 Beacon frame에 존재하며 AP Mac, STA Mac, ANonce, SNonce는 EAPOL frame에 존재한다. 즉 Attacker는 비밀번호를 알고 있다는 것을 가정하에 Beacon과 EAPOL frame을 획득했다면 WPA 환경에서 AP와 특정 Station간에 송수신되는 Data frame의 decrypt가 가능하다.

Wireshark - Edit - Preferences - Protocols - IEEE 802.11 wireless LAN - Decryption keys Edit를 클릭해서 Key type은 wpa-pwd, Key는 \<password\>:\<ssid\> 의 형식으로 추가한다. 이후 aircrack과 마찬가지로 Deauth frame을 전송하여 EAPOL frame을 획득하고, 그 이후 발생하는 Encrypted Data frame에 대해서 decrypt를 할 수 있다. 

## References
https://wiki.wireshark.org/HowToDecrypt802.11

## Youtube
https://youtu.be/KRDKBxrNBzI
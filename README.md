# CVE-2022-38766
PoC for vulnerability in Renault ZOE Keyless System [CVE-2022-38766](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-38766)

### Introduce
![Company_logo](https://www.autocrypt.co.kr/themes/autocrypt/img/header-ci.png)

[AUTOCRYPT](https://autocrypt.io) [[MalHyuk](http://malhyuk.info)]

## Overview
This vulnerability raised the question of whether ZOE electric vehicles are safe form RF hacking. For this reason, the actual ZOE vehicle released this year was targeted and attacked. A study was also conducted on how this attack bypass the rolling codes, a defense technique of RF hacking, and a lot of thought was needed about the handling method in case the car breaks down.



## Attack Scenario
![Attack Scenario](https://i.imgur.com/iXoWjtD.png)

Most cars still open and lock their doors via RF communication. That's why the classic hacking method can open the car's door.



## PoC
My laptop and HackRF are running on the car

### Replay attack
[![Replay attack](https://img.youtube.com/vi/hLcBmIdOJc8/0.jpg)](https://youtu.be/hLcBmIdOJc8)

### DoS attack
[![Replay attack](https://img.youtube.com/vi/VKJQduB2zkU/0.jpg)](https://www.youtube.com/watch?v=VKJQduB2zkU)



## Target Vehicle
```
- Renault 2021 ZOE Electronic car
```

## Key Fob Information
![ZOE Keyfob device](https://i.imgur.com/uFTduLV.png)

```
FCC ID : KR5IK4CH-01
Frequency : 433.92MHz
Modulation : FSK
```
[More Information](https://fccid.io/KR5IK4CH-01)

## Used to
```
- HackRF One + Portapack H2
- GNURadio
- GQRX
- Universal Radio Hacker
- rtl_433
```

## How2Pwn ZOE? (feat. Mitigation)
[Rolling Codes](https://harryli0088.github.io/rolling-code/), otherwise known as hopping code

![rtl_433](https://i.imgur.com/3w3K5Gf.png)

Through this process, we found that the id, flags values are signaled through approximately 8(<=) different values that are fixed. All signals with these values are captured through gnuradio-companion and saved as a file. And you can continue to send signals based on that file. 

When a signal is detected data is written as 0 and 1. However, as shown in screenshot, if there is only one stored id value, it has to be sent until the signal is correct, and the open button of the smart key is pressed several times to capture all the stored signals with all ids. So I thought I could bypass the Rolling codes. 

A better way is to analyze the binary code of the signal and send it after coding.

## References
> [nonamecoder/CVE-2022-27254](https://github.com/nonamecoder/CVE-2022-27254)
>
> [Rolling code](https://harryli0088.github.io/rolling-code/)
>
> [Rolling-PWN](https://rollingpwn.github.io/rolling-pwn/)
>
> [Renault ZOE](https://www.renault.co.uk/electric-vehicles/zoe.html)


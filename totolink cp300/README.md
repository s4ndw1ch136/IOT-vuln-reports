# TOTOLINK CP300 V2.0.4-B20201102  hardcode

### Product Information

Product: TOTOLINK CP300 Firmware Version: V2.0.4-B20201102   Manufacturer's website information：https://www.totolink.net/ 

Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/120/ids/36.html

### Analysis

There is a hard code password for root in /etc/shadow.sample.

![image-20240601184833493](./image-20240601184833493.png)

The decrypted password is root.

![image-20240601184623244](./image-20240601184623244.png)


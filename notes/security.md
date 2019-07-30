# Security

* https://tpbclean.com/
* https://media.defcon.org/
* http://0day.today/
* https://www.bountysource.com/
* https://0x00sec.org/

## Wifi

* [LinSSID: Graphical wireless scanning for Linux](https://sourceforge.net/projects/linssid/)

## Web

* [check web sec > webhint](https://webhint.io/)

## Tools

* Tamper Data
* [Modify Headers](https://addons.mozilla.org/en-US/firefox/addon/modify-headers/)
* [HackBar](https://addons.mozilla.org/en-US/firefox/addon/hackbar/)
* [iMacros]
* [XSStrike: ابزاری اپن‌سورس به منظور تشخیص حملات XSS](https://sokanacademy.com/blog/9137/ایکس-اس-اس-استرایک-ابزاری-اپن‌سورس-به-منظور-تشخیص-حملات-ایکس-اس-اس)

```shell
nmap -PR //ARP Scan
netdiscover
nc //netcap
amap //like nc
pof -i eth0 //sniffing pof
xprobe2 //Find OS
msf //metasploit
msf payload //metasploit payload
smb // so scan
```

### Web Apps

* BurpS
* Metasploit
* Nexpose
* DVWA
* Webgoat
* Acunetix or Netsparker
* BeEF project

### Mobile Apps

* BurpS
* DIVA Android
* MobSF
* AppUse (commercially available)
* Drozer

## Tutorial

* [free class for web security](https://www.hacker101.com/)

## Projects

* [Electronics Project – Simple Card Read Keyboard Emulator Using Arduino Pro Micro](https://www.szehau.com/archives/2015/04/electronics-project-simple-card-read-keyboard-emulator-using-arduino-pro-micro/)

## RF

* https://v3gard.com/tag/rfcat/
* https://leonjza.github.io/blog/2016/10/02/reverse-engineering-static-key-remotes-with-gnuradio-and-rfcat/
* http://dani.foroselectronica.es/rfcat-ti-chronos-and-replaying-rf-signals-337/
* http://leetupload.com/blagosphere/2014/02/16/you-know-how-to-send-my-signal-setting-up-rfcat-from-scratch/
* https://www.legacysecuritygroup.com/index.php/categories/13-sdr/22-rfpwnon-py-the-ultimate-rfcat-ask-ook-brute-force-tool
* https://www.blackhat.com/us-17/training/software-defined-radio.html
* https://console-cowboys.blogspot.com/2017/10/hacking-everything-with-rf-and-software.html
* https://www.shodan.io/
* https://www.hacker101.com/
* http://www.bluehatil.com/abstracts.html
* https://ctftime.org/ctf-wtf/
* https://www.cybersecuritychallenge.org.uk/
* http://onhex.ir/

### HackingRF

* https://andrewmohawk.com/2015/08/31/hacking-fixed-key-remotes-with-only-rfcat/
* https://andrewmohawk.com/2012/07/15/rtlsdr-my-first-sdr/
* https://www.andrewmohawk.com/2012/09/06/hacking-fixed-key-remotes/
* https://www.andrewmohawk.com/2017/02/14/remote-jamming-detector-on-the-cheap/

### RFCAT

```py
from rflib import *
D = RfCat()
d.setFreq(433929000)
d.setFreq(315860000)
d.setMdmModulation(MOD_ASK_OOK)
d.setMdmDRate(4800)
d.setMdmDRate(int(1.0/0.00855))
d.Rfxmit('hex code here')


Rfpwnon.py -f 310000000 -b 1010 -p 100101 -l 10 -r 2
```

## Brute Force

## Command Execution

## CSRF

## File Inclusion

```shell
gdb
disassemble main
set disassembly-flavor intel //make it readble
disassemble main

break *main
run
```

## SQL Injection

## SQL Injection (Blind)

## Shell Uploading

## XSS ( Reflected )

## XSS ( Stored)
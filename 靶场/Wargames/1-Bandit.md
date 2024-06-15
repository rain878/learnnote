# **Bandit**

来自[Wargames](https://overthewire.org/wargames/bandit/)

练习ssh和linux操作

## Level0

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
密码：bandit0

bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
bandit0@bandit:~$
```

## Level1

```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
密码：NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-  #使用相对路径，可以查看特殊文件名
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
bandit1@bandit:~$
```

## Level2

```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
密码：rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

bandit2@bandit:~$ ls -l
total 4
-rw-r----- 1 bandit3 bandit2 33 Oct  5  2023 spaces in this filename
bandit2@bandit:~$ cat spaces\ in\ this\ filename #使用\转移特殊字符
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
bandit2@bandit:~$
```

## Level3

```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org
密码：aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

bandit3@bandit:~$ ls -al inhere/
total 12
drwxr-xr-x 2 root    root    4096 Oct  5  2023 .
drwxr-xr-x 3 root    root    4096 Oct  5  2023 ..
-rw-r----- 1 bandit4 bandit3   33 Oct  5  2023 .hidden
bandit3@bandit:~$ cat inhere/.hidden  #查看隐藏文件
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
bandit3@bandit:~$
```

## Level4

```bash
ssh -p 2220 bandit4@bandit.labs.overthewire.org
密码：2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

bandit4@bandit:~$ file inhere/*
inhere/-file00: data
inhere/-file01: data
inhere/-file02: data
inhere/-file03: data
inhere/-file04: data
inhere/-file05: data
inhere/-file06: data
inhere/-file07: ASCII text  #找到不同的文件类型
inhere/-file08: data
inhere/-file09: data
bandit4@bandit:~$ cat inhere/-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
bandit4@bandit:~$
```

## Level5

提示找大小1033bytes且没有可执行权限的文件

```bash
ssh -p 2220 bandit5@bandit.labs.overthewire.org
密码：lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

bandit5@bandit:~$ find inhere/ -size 1033c ! -executable
inhere/maybehere07/.file2
bandit5@bandit:~$ cat inhere/maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
bandit8@bandit:~$
```

## Level6

```bash
ssh -p 2220 bandit6@bandit.labs.overthewire.org
密码：P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
bandit6@bandit:~$
```

## Level7

```bash
ssh -p 2220 bandit7@bandit.labs.overthewire.org
密码：z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

bandit7@bandit:~$ cat data.txt | grep millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP
bandit8@bandit:~$
```

## Level8

```bash
ssh -p 2220 bandit8@bandit.labs.overthewire.org
密码：TESKZC0XvTetK0S9xNwm25STk5iWrBvP

bandit8@bandit:~$ cat data.txt | sort | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
bandit8@bandit:~$
```

## Level9

```bash
ssh -p 2220 bandit9@bandit.labs.overthewire.org
密码：EN632PlfYiZbn3PhVK3XOGSlNInNE00t

bandit9@bandit:~$ strings data.txt | grep =
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
bandit9@bandit:~$
```

## Level10

```bash
ssh -p 2220 bandit10@bandit.labs.overthewire.org
密码：G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==
bandit10@bandit:~$ cat data.txt | base64 -d
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
bandit10@bandit:~$
```

## Level11

```bash
ssh -p 2220 bandit10@bandit.labs.overthewire.org
密码：6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m' #使用tr命令构造ROT13加解密
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

## Level12

```bash
ssh -p 2220 bandit12@bandit.labs.overthewire.org
密码：JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

解密过程：xdd->gzip->bzip2->gzip->tar->tar->tar->gzip
bandit12@bandit:/tmp/bandit12$ xxd -r data.txt data.out
继续解压
bandit12@bandit:/tmp/bandit12$ cat data8
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```

## Level13

```bash
ssh -p 2220 bandit13@bandit.labs.overthewire.org
密码：wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

bandit13@bandit:~$ ssh -i ./sshkey.private bandit14@localhost -p 2220
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
bandit14@bandit:~$
```

## Level14

```bash
ssh -p 2220 bandit14@bandit.labs.overthewire.org
密码：fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

bandit14@bandit:~$ nc localhost 30000 
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```

## Level15

```bash
ssh -p 2220 bandit15@bandit.labs.overthewire.org
密码：jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
#使用openssl连接服务器或者
openssl s_client -connect localhost:30001 -ign_eof
bandit15@bandit:~$ openssl s_client -connect localhost:30001
read R BLOCK
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1
closed
bandit15@bandit:~$
```

## Level16

```bash
ssh -p 2220 bandit16@bandit.labs.overthewire.org
密码：JQttfApK4SeyHwDlI9SXGR50qclOAil1

bandit16@bandit:~$ nmap -v -sV localhost -p 31000-32000
Discovered open port 31518/tcp on 127.0.0.1
Discovered open port 31046/tcp on 127.0.0.1
Discovered open port 31691/tcp on 127.0.0.1
Discovered open port 31960/tcp on 127.0.0.1
Discovered open port 31790/tcp on 127.0.0.1
bandit16@bandit:~$ openssl s_client -connect localhost:31790
发送本关密码得到Level17的ssh_key，保存到/tmp/tmp_123/123.txt中，权限设置只读
bandit16@bandit:~$ ssh -i /tmp/tmp_123/123.txt bandit17@bandit.labs.overthewire.org -p 2220
bandit17@bandit:~$ cat /etc/bandit_pass/bandit17
VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e
bandit17@bandit:~$
```

## Level17

```bash
ssh -p 2220 bandit17@bandit.labs.overthewire.org
密码：VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e

bandit17@bandit:~$ diff --color passwords.new passwords.old
42c42
< hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
---
> p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW
bandit17@bandit:~$
```

## Level18

```bash
ssh -p 2220 bandit18@bandit.labs.overthewire.org
密码：hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
#一连接会自动断开，可以尝试执行命令
ssh -p 2220 bandit18@bandit.labs.overthewire.org '/bin/bash' #执行一个shell
cat readme
ssh -p 2220 bandit18@bandit.labs.overthewire.org 'cat readme'
awhqfNnAbc1naukrpqDYcF95h7HoMTrC
```

## Level19

```bash
ssh -p 2220 bandit19@bandit.labs.overthewire.org
密码：awhqfNnAbc1naukrpqDYcF95h7HoMTrC
#有一个可执行文件，执行命令
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
```

## Level20

```bash
ssh -p 2220 bandit20@bandit.labs.overthewire.org
密码：VxCazJaVykI6W36BkBU0mJTCM8rR95XT

bandit20@bandit:~$ echo 'VxCazJaVykI6W36BkBU0mJTCM8rR95XT' | nc -l -p 30088 &
[1] 3249375
bandit20@bandit:~$ ./suconnect 30088
Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
Password matches, sending next password
NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
bandit20@bandit:~$
```

## Level21

```bash
ssh -p 2220 bandit21@bandit.labs.overthewire.org
密码：NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
#提示查看定时任务

bandit21@bandit:~$ cd /etc/cron.d
bandit21@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
bandit21@bandit:/etc/cron.d$
```

## Level22

```bash
ssh -p 2220 bandit22@bandit.labs.overthewire.org
密码：WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff

bandit22@bandit:~$ cd /etc/cron.d
bandit22@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:/etc/cron.d$ cat  /usr/bin/cronjob_bandit23.sh
#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@bandit:~$ echo "I am user bandit23" | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
bandit22@bandit:~$
```

## Level23

```bash
ssh -p 2220 bandit23@bandit.labs.overthewire.org
密码：QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
#可以知道这个定时脚本，目的是切换到/var/spool/bandit24文件夹，然后遍历所有文件，并且执行这个文件，如果遇到用户是bandit23的话，先执行，持续一段时间，然后再删除文件
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash
myname=$(whoami)
cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
bandit23@bandit:~$ vim /tmp/123.sh  #读取密码的脚本
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/bandit24_pass
bandit23@bandit:~$ chmod 777 /tmp/123.sh
bandit23@bandit:~$ cp /tmp/123.sh /var/spool/bandit24/foo/
bandit23@bandit:~$ cat /tmp/bandit24_pass
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
bandit23@bandit:~$
```

## Level24

```bash
ssh -p 2220 bandit24@bandit.labs.overthewire.org
密码：VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar

bandit24@bandit:~$ vim /tmp/123.py
#!/usr/bin/python3
# coding: utf-8
import sys
import socket
pincode = 6000
password = "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar"
try:
    # Connect to server
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("127.0.0.1", 30002))
    # Print welcome message
    welcome_msg = s.recv(2048).decode()  # Decode bytes to string
    print(welcome_msg)
    # Try brute-forcing
    while pincode < 10000:
        pincode_string = str(pincode).zfill(4)
        message = password + " " + pincode_string + "\n"
        # Send message
        s.sendall(message.encode())
        receive_msg = s.recv(1024).decode()  # Decode bytes to string
        # Check result
        if "Wrong" in receive_msg:
            print("Wrong PINCODE: %s" % pincode_string)
        else:
            print(receive_msg)
            break
        pincode += 1
finally:
    s.close()  # Close the socket connection
    sys.exit(0)  # Use 0 for normal exit
bandit24@bandit:~$ python3 /tmp/123.py
Wrong PINCODE: 9014
Correct!
The password of user bandit25 is p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d

Exiting.
bandit24@bandit:~$
```

## Level25

```bash
ssh -p 2220 bandit25@bandit.labs.overthewire.org
密码：p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d
#目录下看到bandit26的ssh_key，复制下来改700权限，连接bandit26会自动退出

bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@bandit:~$
bandit25@bandit:~$ cat /usr/bin/showtext #看到bandit26账号的shell路径
#!/bin/sh
export TERM=linux
exec more ~/text.txt  #由于执行了more，所以把窗口调小，more就不会全部显示出来，可以进行编辑模式
exit 0
bandit25@bandit:~$
#登录bandit26会，卡住在more的显示画面，进入编辑模式
:e /etc/bandit_pass/bandit26
c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1
```

## Level26

```bash
ssh -p 2220 bandit26@bandit.labs.overthewire.org
密码：c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1
#如上一题手法，进入编辑模式，进行提权
:set shell sh=/bin/sh
sh
$ ls -alh
total 44K
drwxr-xr-x  3 root     root     4.0K Oct  5  2023 .
drwxr-xr-x 70 root     root     4.0K Oct  5  2023 ..
-rw-r--r--  1 root     root      220 Jan  6  2022 .bash_logout
-rw-r--r--  1 root     root     3.7K Jan  6  2022 .bashrc
-rw-r--r--  1 root     root      807 Jan  6  2022 .profile
drwxr-xr-x  2 root     root     4.0K Oct  5  2023 .ssh
-rwsr-x---  1 bandit27 bandit26  15K Oct  5  2023 bandit27-do #可执行文件，提权
-rw-r-----  1 bandit26 bandit26  258 Oct  5  2023 text.txts
$ ./bandit27-do cat /etc/bandit_pass/bandit27
YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS
$
```

## Level27

```bash
ssh -p 2220 bandit27@bandit.labs.overthewire.org
密码：YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS
#根据提示git，过程需要输入bandit27的密码
bandit27@bandit:~$ mkdir /tmp/git_ssh
bandit27@bandit:~$ cd /tmp/git_ssh
bandit27@bandit:/tmp/git_ssh$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
bandit27@bandit:/tmp/git_ssh$ cat repo/README
The password to the next level is: AVanL161y9rsbcJIsFHuw35rjaOM19nR
bandit27@bandit:/tmp/git_ssh$
```

## Level28

```bash
ssh -p 2220 bandit28@bandit.labs.overthewire.org
密码：AVanL161y9rsbcJIsFHuw35rjaOM19nR
#根据提示git，过程需要输入bandit28的密码
bandit28@bandit:~$ mkdir /tmp/git_ssh
bandit28@bandit:~$ cd /tmp/git_ssh
bandit28@bandit:/tmp/git_ssh$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
bandit28@bandit:/tmp/git_ssh/repo$ git show
commit 14f754b3ba6531a2b89df6ccae6446e8969a41f3 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Oct 5 06:19:41 2023 +0000
    fix info leak
diff --git a/README.md b/README.md
index b302105..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 - username: bandit29
-- password: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S
+- password: xxxxxxxxxx
bandit28@bandit:/tmp/git_ssh/repo$
```

## Level29

```bash
ssh -p 2220 bandit29@bandit.labs.overthewire.org
密码：tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S
#查看git分支
bandit29@bandit:~$ mkdir /tmp/git_3
bandit29@bandit:~$ cd /tmp/git_3
bandit29@bandit:/tmp/git_3$ git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
bandit29@bandit:/tmp/git_3/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
bandit29@bandit:/tmp/git_3/repo$ git checkout dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
Switched to a new branch 'dev'
bandit29@bandit:/tmp/git_3/repo$ git show
commit 1d160de5f8f647f00634bbf3d49b9244275217b6 (HEAD -> dev, origin/dev)
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Oct 5 06:19:43 2023 +0000
    add data needed for development
diff --git a/README.md b/README.md
index 1af21d3..a4b1cf1 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for bandit30 of bandit.
 ## credentials
 - username: bandit30
-- password: <no passwords in production!>
+- password: xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS
bandit29@bandit:/tmp/git_3/repo$
```

## Level30

```bash
ssh -p 2220 bandit30@bandit.labs.overthewire.org
密码：xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS
#查看分支,提交日志,只能查看本地引用
bandit30@bandit:~$ mkdir -p /tmp/git_30
bandit30@bandit:~$ cd /tmp/git_3
bandit30@bandit:/tmp/git_30$ git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
bandit30@bandit:/tmp/git_30$ cd repo
bandit30@bandit:/tmp/git_30/repo$ git show-ref
d39631d73f786269b895ae9a7b14760cbf40a99f refs/heads/master
d39631d73f786269b895ae9a7b14760cbf40a99f refs/remotes/origin/HEAD
d39631d73f786269b895ae9a7b14760cbf40a99f refs/remotes/origin/master
831aac2e2341f009e40e46392a4f5dd318483019 refs/tags/secret
bandit30@bandit:/tmp/git_30/repo$ git show 831aac2e2341f009e40e46392a4f5dd318483019
OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt
bandit30@bandit:/tmp/git_30/repo$
```

## Level31

```bash
ssh -p 2220 bandit31@bandit.labs.overthewire.org
密码：OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt
#根据提示，commit一个key.txt
bandit31@bandit:~$ mkdir /tmp/git_5
bandit31@bandit:~$ cd /tmp/git_5
bandit31@bandit:/tmp/git_5$ git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo
bandit31@bandit:/tmp/git_5/repo$ echo "May I come in?" > key.txt
bandit31@bandit:/tmp/git_5/repo$ git add .
bandit31@bandit:/tmp/git_5/repo$ git commit -m "key.txt"
bandit31@bandit:/tmp/git_5/repo$ git push origin master
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit31/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames
bandit31-git@localhost's password:
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 320 bytes | 320.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: ### Attempting to validate files... ####
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: rmCBvG56y58BXzv98yZGdO7ATVL5dW8y
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
To ssh://localhost:2220/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://localhost:2220/home/bandit31-git/repo'
bandit31@bandit:/tmp/git_5/repo$
```

## Level32

```bash
ssh -p 2220 bandit32@bandit.labs.overthewire.org
密码：rmCBvG56y58BXzv98yZGdO7ATVL5dW8y

$0 的含义

在 Unix-like 系统的 shell 环境中，$0 是一个特殊的变量，用来表示当前正在执行的脚本或命令的名称。如果是在一个脚本中，$0 将显示该脚本的名称；如果是在命令行直接执行的命令，$0 通常显示 shell 的名称或路径。
如何使用 $0 返回正常的 shell

当你在 shell 中输入 $0 并执行时，实际上你是在请求启动一个新的 shell 实例，该实例的类型或路径由 $0 的值决定。例如，如果你在 bash 环境下输入 $0，通常会启动一个新的 bash shell。

>>$0  #进入正常shell
$ cat /etc/bandit_pass/bandit33
odHo63fHiFqcWWJG9rLiLDtPm45KzUKy
$
```

## Level33

```bash
ssh -p 2220 bandit33@bandit.labs.overthewire.org
密码：odHo63fHiFqcWWJG9rLiLDtPm45KzUKy
#游戏结束
bandit33@bandit:~$ cat README.txt
Congratulations on solving the last level of this game!
At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.
If you have an idea for an awesome new level, please let us know!
bandit33@bandit:~$
```


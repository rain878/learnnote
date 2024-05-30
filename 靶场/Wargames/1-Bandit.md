# Bandit

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
```


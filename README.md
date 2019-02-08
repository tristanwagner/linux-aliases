# linux-aliases

---

**Output mongodb logs**

```
alias mdblog='cat /var/log/mongodb/mongod.log'
```

**Restart mongodb**

```
alias mdbrestart='sudo service mongod restart'
```

**Start mongodb**

```
alias mdbstart='sudo service mongod start'
```

**Stop mongodb**

```
alias mdbstop='sudo service mongod stop'
```

**Open mongodb shell**

```
alias mshell='mongo --host 127.0.0.1:27017'
```

**Open bashrc for alias setup**

```
alias openbashrc='nano ~/.bashrc'
```

**Pull repository**

```
alias pull='sudo git pull origin master'
```

**Reload alias configuration**

```
alias bashrc='. ~/.bashrc'
```

**Restart NGINX**

```
alias restartnginx='sudo systemctl reload nginx'
```

**get cwd to clipboard on cmder windows**

```
alias getcd=cd $b clip
```

**edit nginx conf**

```
sudo nano /etc/nginx/sites-available/default
```

**restart php7**

```
sudo systemctl restart php7.0-fpm
```

**check nginx logs**

```
tail -f /var/log/nginx/error.log
```

**find dir**

```
find / -type d -name 'www'
```

**Allow sh script to handle crlf char**

```
bash <(dos2unix < script.sh)
```

**List ip table**

```
iptables -L -n -v
```

**Block ip**

```
iptables -A INPUT -s *.*.*.* -j DROP
```

**public IP**

```
alias ip=curl ipinfo.io/ip
```

[here is more about iptables](http://www.pettingers.org/code/firewall.html)


**look for files related to program**

You can use lsof (list of open files) in most cases to find open log files without knowing the configuration.

Example:

Find the PID of httpd (same concept applies for nginx and other programs):
```
$ ps aux | grep httpd
```
...
```
root     17970  0.0  0.3 495964 64388 ?        Ssl  Oct29   3:45 /usr/sbin/httpd
```
...
Then search for open log files using lsof with the PID:
```
$ lsof -p 17970 | grep log
httpd   17970 root    2w   REG             253,15     2278      6723 /var/log/httpd/error_log
httpd   17970 root   12w   REG             253,15        0      1387 /var/log/httpd/access_log
```
If lsof prints nothing, even though you expected the log files to be found, issue the same command using sudo.


**start process in background, log to file and save pid**

```
nohup <script> >> script.log 2>&1 &
echo $! > save_pid.txt
less +F script.log
```

**stop process**

```
kill -9 `cat save_pid.txt`
rm save_pid.txt
```
# 1. redo last command but as root
sudo !!

# 2. open an editor to run a command
ctrl+x+e

# 3. create a super fast ram disk
mkdir -p /mnt/ram
mount -t tmpfs tmpfs /mnt/ram -o size=8192M

# 4. don't add command to history (note the leading space)
 ls -l

# 5. fix a really long command that you messed up
fc

# 6. tunnel with ssh (local port 3337 -> remote host's 127.0.0.1 on port 6379)
ssh -L 3337:127.0.0.1:6379 root@emkc.org -N

# 7. quickly create folders
mkdir -p folder/{sub1,sub2}/{sub1,sub2,sub3}

# 8. intercept stdout and log to file
cat file | tee -a log | cat > /dev/null

# bonus: exit terminal but leave all processes running
disown -a && exit

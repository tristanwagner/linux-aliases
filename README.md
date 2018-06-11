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

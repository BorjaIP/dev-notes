---
id: 50wwtd36ekpjqvmcblv1upk
title: Linux
desc: ''
updated: 1676886345986
created: 1655319210228
---

- [OS](#os)
  - [Arch](#arch)
  - [Ubuntu](#ubuntu)
- [Users](#users)
- [System info](#system-info)
  - [Kernel](#kernel)
  - [Process](#process)
  - [CPU](#cpu)
  - [Memory](#memory)
  - [Disk](#disk)
  - [Partitions](#partitions)
  - [Services](#services)
  - [Top](#top)
  - [DNS](#dns)
- [Network](#network)
  - [Curl](#curl)
  - [Firewall](#firewall)
  - [Netstat](#netstat)
  - [SS](#ss)
- [GPU](#gpu)
- [SSH](#ssh)
- [Time](#time)
- [Commands](#commands)
- [Java](#java)


## OS

### Arch

[[Arch | os.linux.arch]]

### Ubuntu

[[Ubuntu | os.linux.ubuntu]]

## Users

```bash
# Change to su user
su -

sudo useradd -m user_name
sudo passwd user_name

usermod -aG docker user_name

useradd -u 1000 -g 1 -m -d /home/idmuser -c "Usuario IDMuser" -s /usr/bin/sh idmuser

# last users access to machine
last | head -n 10
```

## System info

```bash
cat /etc/*release

uname -m && cat /etc/*release

cat /etc/os-release
```

### Kernel

```bash
lsb_release -a
```

### Process

```bash
ps -fea
ps fax
ps aux

ps -e -o pid,args | grep dvc | grep -v grep | awk '{print $1}'

# proc file
pid=1825
ls -1 /proc/$pid/fd/*
awk '!/\[/&&$6{_[$6]++}END{for(i in _)print i}' /proc/$pid/maps
ls -l /proc/*/fd
```

### CPU

(Threads x Cores) x Physical CPU = Number vCPU

```bash
less /proc/cpuinfo
lscpu
```

### Memory

```bash
cat /proc/meminfo
free -mht
vmstat -saS M
```

### Disk

```bash
# Todo en carpetas
sudo du -h --max-depth=1 | sort -hr | more
# Carpetas de otra forma
du -s * | sort -nk 1 | awk '{print $2}' | xargs du -hs

du -h -d 1 . | sort -hr

df -h /home
du -bsh /home
du -h
du -sh ./*/ | sort -hr
```

### Partitions

```bash
lsblk
sudo fdisk -l
sfdisk -ls /dev/sda
sudo parted -l
```

### Services

```bash
# See all services running
sudo service --status-all
sudo systemctl --type=service
sudo systemctl --type=service --state=running
# Stop|Start|Status services
sudo service <NAME> status|stop|start
sudo systemctl status|stop|start|enable|disable|is-enabled <NAME>
# show options service
sudo systemctl cat <NAME>
# List unit files (see also if a service is enabled)
sudo systemctl list-unit-files
sudo systemctl list-units --type service
sudo systemctl list-units --state failed
sudo systemctl list-units --state failed --type service
```

---

### Top

+ 1 - muestra los cores
+ c - mostrar path absoluto
+ E - cambiar a MB/GB (arriba)
+ e - cambiar a MB/GB (en la tabla)
+ k - kill programa con PID XXXX
+ h - help
+ H - threads/tasks
+ I - show the overall percentage of available CPUs in use (if not top show the accumulate over all the CPUs)

### DNS

Introducir aqui el DNS (IP del dispositivo)

```bash
 /etc/resolv.conf
```

---

## Network

```bash
# Test conectivity
curl -v telnet://$IP:$PORT

# See traffic route
traceroute 10.210.7.9

# Test internet connection
curl -I https://www.google.com

# show ips
ip r
# show IP and mask
ip addr
ip -4 -o address

# show ports in use
lsof -i -P -n
sudo lsof -iTCP -sTCP:LISTEN -P
lsof -p process-id

# see DNS redirection
nslookup URL

# see red in specific port
tcpdump -i any port 443

# docker network
ifconfig docker0 | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}'
```

### Curl

```bash
curl http://example:5000/ -o /dev/null -s -w '%{http_code}\n'
```

### Firewall

**IPTables**

```bash
# show tables
iptables -L INPUT -n -v
iptables -L OUTPUT -n -v

# add ports
sudo iptables -A INPUT -s 10.0.0.0/8 -p tcp --dport 8080 -j ACCEPT
sudo iptables -A INPUT -p tcp --match multiport --dports 1024:3000 -j ACCEPT

# add IPs ranges
sudo iptables -A INPUT -s 10.0.0.0/8 -j ACCEPT
sudo iptables -A INPUT -m range --src-range 192.168.0.1-192.168.0.255 -j ACCEPT
```

**Firewall-cmd**

```bash
# Firewall CentOS
systemctl status|stop|start firewalld
firewall-cmd --state
# Show all the information
firewall-cmd --list-all
firewall-cmd --list-ports
firewall-cmd --list-all-zones 
firewall-cmd --get-active-zones
firewall-cmd --get-default-zone 
firewall-cmd --check-config
# show trafic
firewall-cmd --get-default-zone
firewall-cmd --get-active-zones
# Remove port
firewall-cmd --zone=public --remove-port=10050/tcp
# Add port to firewall
firewall-cmd --permanent --add-port=5000/tcp
firewall-cmd --reload
# Add port for RDP
firewall-cmd --permanent --zone=public --add-port=3389/tcp
# SAVE ALWAYS THE CHANGES
firewall-cmd --runtime-to-permanent 
firewall-cmd --reload 
```

**UFW**

```bash
# Debian
ufw allow 5000
```

### Netstat

```bash
netstat -nr
netstat -ai
netstat -ant
netstat -pnltu
netstat -pluton
netstat putona
```

### SS

```bash
ss -tapn
ss -dst :https
ss -dst :5432
```

---

## GPU

```bash
watch -n0.1 nvidia-smi

nvidia-smi -l 2
```

## SSH

```bash
mkdir ~/.ssh && chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
# copy you plubic key inside authorized_keys
ssh-copy-id -i ~/.ssh/id_rsa.pub usuario@ipdestino
# generate custom key
ssh-keygen -f name
# see access
grep -i Failed /var/log/secure

# see access machine IP users
last -a | grep -i still
w
# show last users
last -a
```

## Time

```bash
# list time
timedatectl
# set time
sudo timedatectl set-time 15:00:00
```

---

## Commands

```bash
# find a word in a multiple files    
grep -irl word
# find a file 
find -name *.sh
# remove all files in directories and subdirectores
find . -name \*.html -type f -delete
# RDP
port 3389
# add /usr/local/bin
export PATH=$PATH:/usr/local/bin
# instead of cp for show progress
rsync -avz
```

## Java
```bash
# show memory usage
jmap -heap 13129
```

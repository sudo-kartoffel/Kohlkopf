# Tous les packages dont on aura besoin :

```
dnf update -y
dnf upgrade -y
dnf install vim
dnf install iptables iptables-services -y
dnf install tcpdump
```

# System config

## Run on boot

```
chown root:root /etc/rc.local
chmod 700 /etc/rc.local
```

# Network Config 

## Hostname

```
hostnamectl set-hostname red
```

## Interfaces and routing

nmtui config

```
enp0s3
ipv4 auto
ipv6 disabled
```

```
enp0s8
ipv4 manual
addresses 172.16.2.1/30
Routing 172.16.0.0/23 via 172.16.2.2
[X]Require IPv4 addressing for this connection

ipv6 disabled

[x] Auto connect
[x] Available to all
```

```
systemctl restart NetworkManager
nmcli
```

## Forwarding /etc/sysctl.conf

```
vim /etc/sysctl.conf

net.ipv4.ip_forward=1

service systemd-sysctl restart
```

# Firwalling

```
systemctl disable --now firwalld
systemctl enable --now iptables
echo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE > /etc/
```

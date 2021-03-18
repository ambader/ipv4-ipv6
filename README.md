# ipv4-ipv6

Socat connect IPv4 to IPv6
  based on https://www.mbuth.de/?p=1356

create socat directory
```console
mkdir /etc/socat
```

load shell scripts
```console
wget https://raw.githubusercontent.com/ambader/ipv4-ipv6/main/shell_http -O /etc/socat/80_socat
wget https://raw.githubusercontent.com/ambader/ipv4-ipv6/main/shell_https -O /etc/socat/443_socat
```

replace [::1] by IPv6 of target server
```console
nano /etc/socat/80_socat
#/usr/bin/socat TCP4-LISTEN:80,fork TCP6:[::1]:80 

nano /etc/socat/443_socat
#/usr/bin/socat TCP4-LISTEN:443,fork TCP6:[::1]:443
```

make scripts executable
```console
chmod 755 /etc/socat/80_socat && chmod 755 /etc/socat/443_socat
```

load service scripts
```console
wget https://raw.githubusercontent.com/ambader/ipv4-ipv6/main/service_http -O /etc/systemd/system/80_socat.service
wget https://raw.githubusercontent.com/ambader/ipv4-ipv6/main/service_https -O /etc/systemd/system/443_socat.service
```

reload daemon and start services
```console
systemctl daemon-reload
systemctl start 80_socat && systemctl start 443_socat
```

start services after boot
```console
systemctl enable 80_socat && systemctl enable 443_socat
```

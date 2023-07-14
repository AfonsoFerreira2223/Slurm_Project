
## This should be done on all nodes and controller:

```
apt install munge libmunge2 libmunge-dev

chown -R munge: /etc/munge/ /var/log/munge/ /var/lib/munge/
chmod 0700 /etc/munge/ /var/log/munge/ /var/lib/munge/
```

### Controller:

```
cd etc/munge
python3 -m http.server
```

### Clients:

```
cd /etc/munge
rm munge.key
wget [Controller's Private IP]:8000/munge.key
```

```
systemctl enable munge
systemctl start munge
```


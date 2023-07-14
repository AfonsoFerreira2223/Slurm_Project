## NODE

    sudo su
    apt update & upgrade -y


Change the hostname:

```
hostnamectl set-hostname node1

```

**Don't forget to update the `/etc/hosts` file**

```
apt install slurm-wlm

cd /etc/slurm
```


## If you used method **1** to create the slurm.conf file:

Go to your controller and move your slurm.conf file to the /usr/share/doc/slurmctld folder, then start the web server:

```
cd /etc/slurm/slurm.conf
cp slurm.conf /usr/share/doc/slurmctld/
cd /usr/share/doc/slurmctld/
chmod +r slurm-wlm-configurator.html
python3 -m http.server
```

Now go back to the client:

```
wget [Controller's Private IP]:8000/slurm.conf
```

Do the same with the cgroup.conf:

```
wget [Controller's Private IP]:8000/cgroup.conf
```

#

## If you used method **2** to create the slurm.conf file:


Go to the slurm.conf file and paste it into:

    nano /etc/slurm/slurm.conf

**(This assumes you already made the changes to the file when creating it on the controller.)**
   


And do the same with the `cgroup.conf` file


```
nano /etc/slurm/cgroup.conf
```


#

Start the slurm service

```
systemctl daemon-reload
systemctl start slurmd
systemctl status slurmd
```

Just to make sure, disable slurmctld on the client since it may create problems:

```
systemctl disable slurmctld
```



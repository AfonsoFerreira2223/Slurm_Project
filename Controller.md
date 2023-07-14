# Machines:


This project was created using two machines on aws running ubuntu 20.04. Don't forget to set the security group rules to allow traffic to/between your machines. The machine types were t2.medium, which has 2 cpu and should be more than enough to run slurm commands.


## Controller:

Start by updating the machine:


    sudo su
    apt update & apt upgrade -y

The first step is to set your hostname:

```
hostnamectl set-hostname controller
```


**You will change the hostname of every host, nodes and controller. As such, it's important to change the `/etc/hosts` to be the same across every node and make sure each machine can recognize each other through their hostnames.**

An example using one controller (controller) and one node (node1) with IP addresses 172.31.89.139 and 172.31.80.16 respectively:


![image](https://github.com/AfonsoFerreira2223/Slurm_Project/assets/114146560/472dc5e3-4e2b-4df7-b8a7-4f2f60592662)


You can check the machines' hostname and Ip address with the commands `hostname` and `ip a`.


**Don't forget to keep `/etc/hosts` updated every time you make a change on one of the slurm nodes.**


Now that your slurm controller has a hostname (I will be using the name 'controller' here for simplicity's sake) you can install slurm

```
apt install slurm-wlm
```

Got to the slurm default folder:

    cd /etc/slurm

Now you have to create the file slurm.conf


There are two ways to edit this file.

#### 1:

```
cd /usr/share/doc/slurmctld/
chmod +r slurm-wlm-configurator.html
python3 -m http.server
```

This will open a :8000 connection, replace the Ip 0.0.0.0 with your IP address (public address, you can find this in your aws instance details page on the aws EC2 site) and paste this in your web browser.


The page should look something like this:

![image](https://github.com/AfonsoFerreira2223/Slurm_Project/assets/114146560/17444911-573c-43fc-9036-32648f507297)

You can choose one of the slurm-wlm-configurator.html and create your slurm.conf file from a template

Then paste the conf into 

    nano /etc/slurm/slurm.conf


Then on the client, use wget to grab the configuration from the server. (Refer to client.md for this)


#### 2

This method doesn't involve using the official slurm configurator.

Go to the slurm.conf (controller) file and paste it into a text editor. Make the necessary changes to the template. 


 
Then place the file in

    nano /etc/slurm/slurm.conf


Next, go to the cgroup.conf and copy-paste its content to


```
nano cgroup.conf
```

Create this file:

```
nano slurmd.service
```

And then check the status of slurm

```
systemctl daemon-reload
systemctl start slurmd
systemctl status slurmd
```

Now install iptables:


```
sudo apt install iptables
sudo apt install netfilter-persistent
```

And make the following configurations to `sudo nano /etc/iptables/rules.v4`

*Refer to the iptables file on your left*

```
netfilter-persistent reload
netfilter-persistent save
```


The last step on the controller is to install munge 

*refer to munge_config file*

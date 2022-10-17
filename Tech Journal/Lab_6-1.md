# Lab 6-1: Port Forwarding and Jump Boxes

## Netplan configuration for Ubuntu
```
network:
  ethernets:
    ens160:
      addresses:
        - 172.16.50.4/29
      nameservers:
        addresses: [172.16.50.2]
      routes:
        - to: default
          via: 172.16.50.2
  version: 2
```
## Port Forwarding
```
description HTTP->WEB01
 destination {
     port 80
 }
 inbound-interface eth0
 protocol tcp
 translation {
     address 172.16.50.3
     port 80
 }
```

## Passwordless User

### Keypair generation
* `ssh-keygen -C jump-jack -f jump-jack`

### passwordless user/key-based ssh
* `sudo -i`
* `adduser --disabled-password jack`
* `mkdir /home/jack/.ssh`
* `touch /home/jack/.ssh/authorized_keys`
* `chown -R jack:jack /home/jack/.ssh`
* `chmod 700 /home/jack/.ssh`
* `chmod 600 /home/jack/.ssh/authorized_keys`
* Copy/paste public key into jack-public-key.txt
* `cat jack-public-key.txt >> /home/jack/.ssh/authorized_keys`
* `echo "PubkeyAuthentication yes" >> /etc/ssh/sshd_config`
* `systemctl restart sshd`
* `exit`
> This method did not work for me, I verified the network settings but each attempt to make a connection would time out.

## Agent Installation

### On mgmt01
* `curl -so wazuh-agent-4.3.7.deb https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.3.7-1_amd64.deb`
* `scp wazuh-agent_4.3.7-1_amd64.deb jack@172.16.50.4:/home/jack`

### On Jump
* `sudo WAZUH_MANAGER='172.16.200.10' WAZUH_AGENT_GROUP='default' dpkg -i ./wazuh-agent-4.3.7.deb`
* `sudo systemctl daemon-reload`
* `sudo systemctl enable wazuh-agent`
* `sudo systemctl start wazuh-agent`
> This also didn't work for me, I was able to get the service installed and running but was unable to see the agent in the Wazuh console.

## Reflection
The biggest challenge I faced in this lab was passwordless ssh. I am unsure why I was having such difficulty, as I verified the firewall settings and followed Devin's example when I was stuck. This is certainly something that I will look further into on my own time. I was also struggling with the Wazuh agent installation. I suspect this is due to a firewall rule that I have not caught, but I am pretty certain that the proper ports and addresses are allowed through on the proper interfaces. I will need to further evaluate what happened here before the assessment.

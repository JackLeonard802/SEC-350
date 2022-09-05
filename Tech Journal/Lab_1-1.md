# Lab 1.1

## Steps

* Configure Road Warrior box
* Configure VyOS firewall
  * VyOS uses similar commands to cisco
* Configure CentOS web server
* Configure NAT and DNS forwarding on fw01
* Configure log01
  * In log01 firewall needed to be reloaded after allowing 514/tcp and 514/udp
  * In the future, always reload the firewall
* install httpd on web01
* configure rsyslog on log01
* configure web01 as rsyslog client


## VyOS

### Commands used

* configure, commit, save, exit, repeat
* set system host-name fw01-jack
* show interfaces
* delete interfaces ethernet eth0 address dhcp
* set interfaces ethernet eth0 description SEC350-WAN
* set interfaces ethernet ethX address IPADDRESS/MASK
* set protocols static route 0.0.0.0/0 next-hop 10.0.17.2
* set system name-server 10.0.17.2

## rsyslog

### Host config

* open port 514/TCP and 514/UDP
* edit /etc/rsyslog.conf
* restart rsyslog

### Client config

* create /etc/rsyslog/sec350.conf
* add line user.notice @172.16.50.5
  * user=syslog facility
  * notice=syslog priority
  * @=UDP, @@ means TCP, so we are only going to send UDP
  * 172.16.50.5=Remote Syslog Server
* tail -f /var/log/messages on log01 to test

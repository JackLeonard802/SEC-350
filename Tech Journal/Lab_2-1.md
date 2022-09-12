# Lab 2.1

## Mgmt01

* Place mgmt01 on LAN
* Assign IP
* Install Chrome Remote Desktop on mgmt01

## Log01

* Restore changes in /etc/rsyslog.conf
* Create 03-sec350.conf file
* Restart and test rsyslog

### Install Tree

`yum install tree -y`

## Web01

* Modify rsyslog client configuration so authentication events are forwarded to log01
* Restart the rsyslog service

## Fw01

### Commands to forward authentication messages from fw01 to log01

* `set system syslog host [*ip*] facility authpriv level info`
* `commit`
* `save`

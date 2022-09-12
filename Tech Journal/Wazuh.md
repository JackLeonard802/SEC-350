# Wazuh!

## Server Installation

* `curl -sO https://packages.wazuh.com/4.3/wazuh-install.sh && sudo bash ./wazuh-install.sh -a`
  * Note admin password, write it down because it is very long and randomized
* Open firewall ports
  * `sudo firewall-cmd --permanent --add-port={1515/tcp,1514/tcp,514/tcp,514/udp,55000/tcp,443/tcp}`
  * `sudo firewall-cmd --reload`
* Access Wazuh from web browser


## Agent Installation (CentOS)

* Navigate to agents screen in Wazuh, deploy new agent
  1. Redhat/CentoS
  2. CentOS 6 or higher
  3. x86_64
  4. *server ip*
  5. default
  6. Run commands on target system
    * `sudo WAZUH_MANAGER='172.16.150.5' WAZUH_AGENT_GROUP='default' yum install https://packages.wazuh.com/4.x/yum/wazuh-agent-4.3.7-1.x86_64.rpm`
    * `sudo systemctl daemon-reload`
    * `sudo systemctl enable wazuh-agent`
    * `sudo systemctl start wazuh-agent`
* Agent files are stored in /var/ossec/etc/ossec

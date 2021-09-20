# zabbix-install
!#/bin/bash
dnf install https://repo.zabbix.com/zabbix/5.4/rhel/8/x86_64/zabbix-agent-5.4.0-8.el8.x86_64.rpm -y;
grep 'Server=127.0.0.1' -P -R -I -l /etc/zabbix/zabbix_agentd.conf | xargs sed -i 's/Server=127.0.0.1/Server=192.168.0.10/g';
systemctl restart zabbix-agent;
firewall-cmd --add-service={http,https} --permanent;
firewall-cmd --add-port={10051/tcp,10050/tcp} --permanent;
firewall-cmd --reload

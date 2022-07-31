# install zabbix-proxy in ubuntu
```
 wget  https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-1+ubuntu20.04_all.deb
 dpkg -i zabbix-release_6.0-1+ubuntu20.04_all.deb
  apt update 
apt-get install zabbix-proxy-mysql zabbix-sql-scripts  

# Install MariaDB
sudo apt -y install mariadb-common mariadb-server mariadb-client
systemctl start mariadb
sudo systemctl enable mariadb

 #zcat /usr/share/zabbix-proxy-mysql/schema.sql.gz | mysql -u zabbix zabbix -p

mysql << EOF  
create database zabbixproxy character set utf8mb4 collate utf8mb4_bin;
create user zabbix@localhost identified by 'zabbixdb';
grant all privileges on zabbixproxy.* to zabbix@localhost;
EOF

cat /usr/share/doc/zabbix-sql-scripts/mysql/proxy.sql  | mysql -u zabbix zabbixproxy -p


vim /etc/zabbix/zabbix_proxy.conf

DBHost=localhost
DBName=zabbixproxy
DBUser=zabbix
DBPassword=zabbixdb
Server=10.7.44.235 (IP ADDRESS OF ZABBIX SERVER)
Hostname=Zabbix-proxy-1

service zabbix-proxy start
```

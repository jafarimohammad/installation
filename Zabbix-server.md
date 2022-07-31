# install Zabbix from source code on ubuntu
```
apt update
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-1+ubuntu20.04_all.deb
dpkg -i zabbix-release_6.0-1+ubuntu20.04_all.deb

apt install gcc libssh2-1-dev golang make odbc-mariadb unixodbc unixodbc-dev odbcinst mysql-server zabbix-agent2 libxml2-dev pkg-config libsnmp-dev snmp  libopenipmi-dev libevent-dev  libcurl4-openssl-dev libpcre3-dev build-essential libmariadb-dev sudo libxml2-dev snmp libsnmp-dev libcurl4-openssl-dev php-gd php-xml php-bcmath php-mbstring vim libevent-dev libpcre3-dev libxml2-dev libmariadb-dev libopenipmi-dev pkg-config php-ldap php-mysql -y

cd /opt

export PATH=$PATH:/usr/local/go/bin

wget https://cdn.zabbix.com/zabbix/sources/stable/6.0/zabbix-6.0.3.tar.gz
 tar -zxvf zabbix-6.0.3.tar.gz 

addgroup --system --quiet zabbix 
adduser --quiet --system --disabled-login --ingroup zabbix --home /var/lib/zabbix --no-create-home zabbix
mkdir -m u=rwx,g=rwx,o= -p /var/lib/zabbix
chown zabbix:zabbix /var/lib/zabbix
cd zabbix-6.0.3/

 ./configure --enable-server --enable-agent --with-mysql --enable-ipv6 --with-unixodbc --with-net-snmp --with-libcurl --with-libxml2 --with-openipmi  --enable-agent2 --with-ssh2
make install
apt update 
apt install  zabbix-frontend-php mysql-server zabbix-nginx-conf zabbix-sql-scripts nginx -y 

cp  conf/zabbix_server.conf  /etc/zabbix/
cp /etc/zabbix/nginx.conf /etc/nginx/sites-enabled/zabbix.conf
echo -n "[Unit]
Description=Zabbix Server
After=syslog.target network.target mysql.service

[Service]
Type=simple
User=zabbix
ExecStart=/usr/local/sbin/zabbix_server -c /etc/zabbix/zabbix_server.conf
ExecReload=/usr/local/sbin/zabbix_server -R config_cache_reload
RemainAfterExit=yes
PIDFile=/tmp/zabbix_server.pid

[Install]
WantedBy=multi-user.target" > /etc/systemd/system/zabbix-server.service



 systemctl enable  zabbix-server
  systemctl enable  nginx
   systemctl enable  zabbix-agent
 systemctl daemon-reload
 mysql << EOF  
create database zabbix character set utf8mb4 collate utf8mb4_bin;
create user zabbix@localhost identified by 'zabbixdb';
grant all privileges on zabbix.* to zabbix@localhost;
EOF

zcat /usr/share/doc/zabbix-sql-scripts/mysql/server.sql.gz | mysql -uzabbix -p zabbix 
 echo "DBPassword=zabbixdb" >> /etc/zabbix/zabbix_server.conf

systemctl restart zabbix-server 
systemctl restart nginx
systemctl restart zabbix-agent2
```

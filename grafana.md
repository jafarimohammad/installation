# install grafana in ubuntu
```
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
apt update && apt install  grafana
systemctl enable grafana-server
sudo systemctl start grafana-server

#Zabbix Plugin Installation Way 1 (Doesnt need proxy)
grafana-cli --pluginUrl \
https://github.com/alexanderzobnin/grafana-zabbix/releases/download/v4.2.8/alexanderzobnin-zabbix-app-4.2.8.zip \
plugins install zabbix

#Zabbix Plugin Installation Way 2 (need proxy)
grafana-cli plugins install alexanderzobnin-zabbix-app
```

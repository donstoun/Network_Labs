### MikroTik

/ip dhcp-server print - показать список DHCP-серверов  
/ip dhcp-server disable dhcp1 - отключить DHCP-сервер dhcp1  
/ip address add address=172.16.10.1/24 interface=ether2 - назначить IP на интерфейс второй подсети  
/ip dhcp-relay add name=relay1 interface=ether2 dhcp-server=192.168.10.2 local-address=172.16.10.1 - создать DHCP Relay на MikroTik  
/ip dhcp-relay enable relay1 - включить DHCP Relay  

### Ubuntu (DHCP server isc-dhcp-server)

/etc/default/isc-dhcp-server: INTERFACESv4="ens3" - указать интерфейс для DHCP-сервера  
sudo apt install isc-dhcp-server - установить пакет DHCP-сервера  
sudo nano /etc/dhcp/dhcpd.conf - редактировать конфигурацию DHCP  
(subnet 192.168.10.0 ...) - задать пул и параметры первой подсети  
(subnet 172.16.10.0 ...) - задать пул и параметры второй подсети  
sudo ip addr add 192.168.10.2/24 dev ens3 - назначить статический IP серверу  
sudo systemctl restart isc-dhcp-server - перезапустить сервис DHCP  
sudo dhcp-lease-list - показать текущие аренды  
add address=192.168.10.105 mac-address=0c:a2:21:ee:00:00 comment="Ubuntu fixed IP" server=dhcp1 - создать статическую аренду  

### Windows (клиент)

/ipconfig /release - освободить текущий IP-адрес  
/ipconfig /renew - запросить новый IP-адрес  

### Клиенты Linux (Ubuntu)

/sbin/dhclient - запустить DHCP-клиент для получения IP  


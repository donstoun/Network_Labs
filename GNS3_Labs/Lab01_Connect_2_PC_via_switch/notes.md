# Заметки к Lab 1 — GNS3 (Switch + Windows 10 + Kali Linux)

## Что сделано:
- Развернул топологию в GNS3: Windows 10 и Kali Linux соединены через Cisco IOSv L2 Switch.
- Подключил:
  - Windows 10 → FastEthernet0/1
  - Kali Linux → FastEthernet0/2

![Топология](images/topology.png)

***

![start](images/start.png)

- Назначил статические IP:
  - Windows 10: `192.168.1.2/24`
  - Kali Linux: `192.168.1.3/24`

![set_ip](images/set_ip_win.png)

***

![set_ip](images/set_ip_linux.png)

- Проверил соединение:
  - Сначала `ping` с Windows на Kali проходил, но с Kali на Windows нет.
  - Проблема оказалась в настройках Windows, были отключены входящие ICMP.
  - Включил сетевое обнаружение (network discovery) и разрешил ICMP во входящих правилах брандмауэра.
  - После этого `ping` заработал.

![ping1](images/ping1.png)

***

![share_options](images/share_options.png)

***

![ping2](images/ping2.png)

## Выводы:
- Коммутатор L2 корректно передаёт трафик между портами.
- Для работы ping между хостами:
  - IP-адреса должны быть в одной подсети.
  - ICMP-запросы должны быть разрешены в фаерволе.
- Windows может по умолчанию блокировать входящий ICMP (ping), что надо учитывать при отладке.

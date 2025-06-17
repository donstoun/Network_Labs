# Lab 7 — Связь между двумя подсетями через маршрутизатор

## 🔧 Что сделано:

- Построена сеть с двумя подсетями:
  - Подсеть 1: Windows-клиент — `192.168.10.2/24`, шлюз — `192.168.10.1`
  - Подсеть 2: Fedora-сервер — `172.16.0.10/16`, шлюз — `172.16.0.1`
- Устройства подключены через маршрутизатор:
  - `Router0`:
    - Интерфейс G0/0 — к Windows, IP: `192.168.10.1/24`
    - Интерфейс G0/1 — к Fedora, IP: `172.16.0.1/16`

![topology](images/topology.png)

---

![start](images/start.png)


- Назначены статические IP-адреса и шлюзы.
- Проверена связь (ping, http).

---

## ⚙ Настройка оборудования

### 🔸 Router0 (Cisco IOS)

```bash
enable
configure terminal

interface g0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface g0/1
 ip address 172.16.0.1 255.255.0.0
 no shutdown

end
write memory

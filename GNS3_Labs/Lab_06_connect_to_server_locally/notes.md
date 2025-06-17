# Заметки к Lab 6 - Подключение ПК к серверу в локальной сети

## Что сделано:

- Создана локальная сеть: Windows 10 (клиент) ↔ Fedora Cloud (сервер) через Switch.

![topology](images/topology.png)

---

![start](images/start.png)

- Назначены IP-адреса:
  - Windows 10: 192.168.1.2/24
  - Fedora Cloud: 192.168.1.10/24



- Проверена базовая связность с помощью команды `ping` — пакеты успешно доходят.
- На Fedora-сервере запущен встроенный HTTP-сервер:
  ```bash
  sudo python3 -m http.server 80

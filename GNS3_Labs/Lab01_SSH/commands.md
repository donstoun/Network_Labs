# Команды для настройки сети и оборудования

## 1. Настройка Cisco R1

```bash
enable                             # Вход в режим привилегий
configure terminal                 # Переход в режим глобальной настройки
hostname R1                        # Присваиваем имя устройству
ip domain-name lab.local           # Доменное имя, необходимо для SSH-ключей
```

### Генерация ключей SSH:

```bash
crypto key generate rsa             # Генерация RSA-ключей
```

### Создание пользователя:

```bash
username admin privilege 15 secret test123  # Создаем пользователя с правами администратора
```

### Настройка удалённого доступа:

```bash
line vty 0 4                        # Настройка виртуальных терминалов, до 5 подключений
transport input ssh                 # Разрешаем только SSH-подключения
login local                         # Используем локальную базу для аутентификации
```

### Настройка интерфейсов:

```bash
interface GigabitEthernet0/0
ip address 192.168.10.1 255.255.255.0
no shutdown                         # Включаем интерфейс

interface GigabitEthernet0/1
ip address 10.10.10.1 255.255.255.252
no shutdown
```

### Статический маршрут:

```bash
ip route 172.16.10.0 255.255.255.0 10.10.10.2  # Маршрут к сети второго офиса через MikroTik
```

---

## 2. Настройка MikroTik

### Переименование интерфейсов для удобства:

```bash
/interface ethernet set [find default-name=ether1] name=LAN
/interface ethernet set [find default-name=ether2] name=WAN
```

### Назначение IP-адресов:

```bash
/ip address add address=172.16.10.1/24 interface=LAN
/ip address add address=10.10.10.2/30 interface=WAN
```

### Включение и настройка SSH:

```bash
/ip service enable ssh                               # Включаем SSH-сервис
/ip ssh set strong-crypto=yes allow-none-crypto=no   # Более безопасные шифры, запрещаем слабые
/ip ssh set always-allow-password-login=yes          # Разрешаем аутентификацию по паролю
```

### Ограничение доступа по IP:

```bash
/ip firewall filter add chain=input protocol=tcp dst-port=22 src-address=172.16.10.10 action=accept  # Разрешаем SSH только с Kali
/ip firewall filter add chain=input protocol=tcp dst-port=22 action=drop                              # Остальные блокируем
```

### Маршрут к сети первого офиса:

```bash
/ip route add dst-address=192.168.10.0/24 gateway=10.10.10.1
```

---

## 3. Настройка Kali Linux

### Назначение IP и шлюза:

```bash
ip addr add 172.16.10.10/24 dev eth0    # Назначаем IP-адрес на интерфейс eth0
ip route add default via 172.16.10.1    # Назначаем шлюз по умолчанию (адрес MikroTik)
```

### Подключение по SSH:

```bash
ssh -c aes192-cbc admin@192.168.10.1    # Подключение к Cisco (обязательно указывать шифр)
ssh admin@172.16.10.1                   # Подключение к MikroTik
```

---

## 4. Настройка Windows 10

### Настройка IP вручную:

```
IP-адрес:      192.168.10.10
Маска:         255.255.255.0
Шлюз:          192.168.10.1
```


### Подключение по SSH из CMD:

```cmd
ssh -c aes192-cbc admin@192.168.10.1    # Подключение к Cisco с указанием шифра
ssh admin@172.16.10.1                   # Подключение к MikroTik
```

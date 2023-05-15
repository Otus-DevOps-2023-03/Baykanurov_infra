# Baykanurov_infra
Baykanurov Infra repository

## Cloud Bastion
### VM address
bastion_IP = 158.160.107.73
someinternalhost_IP = 10.128.0.16

### Подключение к someinternalhost
1. Создадим файл `~/.ssh/config`
```bash
touch ~/.ssh/config && chmod 600 ~/.ssh/config
```
2. Запишем в него конфигурацию подключения к bastion и someinternalhost
```bash
Host bastion
HostName 158.160.107.73
User baykanurov

Host someinternalhost
HostName 10.128.0.16
ProxyJump bastion
User baykanurov
```
3. Проверим подключение
```bash
ssh someinternalhost
```
P.S. Конфигурация в файле `~/.ssh/config` также позволяет нам подключаться к bastion
```bash
ssh bastion
```

### Создание VPN-сервера
Скрипт `setupvpn.sh` устанавливает VPN-cервер `pritunl`
```bash
sudo bash setupvpn.sh
```
После установки открываем в браузере https://158.160.107.73/setup и следуем инструкциям
Чтобы получить логин и пароль для входа нужно ввести команду:
```bash
sudo pritunl default-password
```

### Подключение к someinternalhost через VPN
После добавления конфигурационного файла cloud-bastion.ovpn в клиент
OpenVPN, можно проверить успешность подключения командой:
```bash
ssh -i ~/.ssh/id_rsa baykanurov@10.128.0.16
```

![image](https://github.com/user-attachments/assets/4f38ef37-7ec1-4df0-a89b-2e63b5bc62b6)

----
Ставим апаче с кастом страницей на WEB01 и WEB02

```
apt install apache2
```

Кидаем её сюда 👉 /var/www/html/[index.html](https://github.com/Wireflex/Network/blob/36f8db45a1bba9e727d20d0f8be60a77e5244818/HaProxy%7CKeepalived/index.html)

![image](https://github.com/Wireflex/Network/assets/165675775/71c22c76-663b-4b2e-84d1-074d0bf93b98)

Устанавливаем HAProxy и конфигурируем его на LB01 и LB02

```
apt install haproxy
```

Дописываем в конце конфига 👉 /etc/haproxy/[haproxy.cfg](https://github.com/Wireflex/Network/blob/3c20f3e768978ad461492429995c3861ac6909f3/HaProxy%7CKeepalived/haproxy.cfg)

----

![image](https://github.com/user-attachments/assets/7996ff93-2ae3-46a5-9c8d-2b33bc1c7f49)

Устанавливаем keepalived и конфигурируем его на LB01 и LB02

```
apt install keepalived
```

Нужно создать конфиг /etc/keepalived/[keepalived01.conf](https://github.com/Wireflex/Network/blob/d9e95c2483354346ff506ec1314512e083581b22/HaProxy%7CKeepalived/keepalived01.conf) для LB01

и backup для LB02    /etc/keepalived/[keepalived02.conf](https://github.com/Wireflex/Network/blob/d9e95c2483354346ff506ec1314512e083581b22/HaProxy%7CKeepalived/keepalived02.conf)

Создаём пользователя для запуска скрипта

```
useradd -s /usr/bin/nologin keepalived_script
```

Нужно добавить параметр в конфигурации ядра Linux, который разрешает привязывать сокеты к адресам, которые не являются локальными для сетевого интерфейса(для виртуалок или контейнеров)

```
nano /etc/sysctl.conf и вписываем net.ipv4.ip_nonlocal_bind=1

sysctl -p ,включаем
```

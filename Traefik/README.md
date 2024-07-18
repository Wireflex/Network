![image](https://github.com/user-attachments/assets/f0680b4b-d8cd-4eb7-8c6f-4f3b95271439)

Это инструмент, который выполняет функции реверс-прокси и облегчает управление и маршрутизацию трафика в среде Docker. Он предоставляет простой и удобный способ работы с контейнерами, позволяя автоматически проксировать запросы к различным сервисам, исходя из их конфигурации и меток

### [Quick Start - Docker](https://doc.traefik.io/traefik/getting-started/quick-start/)

### [Docker](https://docs.docker.com/compose/install/linux/)
<details> <summary><kbd>Ctrl</kbd>+<kbd>C</kbd> and <kbd>Ctrl</kbd> + <kbd>V</kbd></summary>
  
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER && newgrp docker
sudo apt-get install docker-compose-plugin -y
docker --version
```
</details>

----

Добавляем А-запись *.demo ( все поддоменные имена будут направляться на указанный IP ) 
![image](https://github.com/user-attachments/assets/8ced4e05-3e2e-4088-9376-aea1cdf1a01c)

### [Traefik](https://github.com/Wireflex/Network/blob/2196175a3fe2e6204369bbe2ef7f3c43d0839404/Traefik/traefik-compose.yml)

### [Nginx](https://github.com/Wireflex/Network/blob/2196175a3fe2e6204369bbe2ef7f3c43d0839404/Traefik/nginx-compose.yml)

### [Apache](https://github.com/Wireflex/Network/blob/2196175a3fe2e6204369bbe2ef7f3c43d0839404/Traefik/apache-compose.yml)

### [Grafana](https://github.com/Wireflex/Network/blob/2196175a3fe2e6204369bbe2ef7f3c43d0839404/Traefik/grafana-compose.yml)

### [Whoami](https://github.com/Wireflex/Network/blob/2196175a3fe2e6204369bbe2ef7f3c43d0839404/Traefik/whoami-compose.yml)

### [Mysql](https://github.com/Wireflex/Network/blob/2196175a3fe2e6204369bbe2ef7f3c43d0839404/Traefik/mysql-compose.yml)

## [Final docker-compose.yml](https://github.com/Wireflex/Network/blob/2196175a3fe2e6204369bbe2ef7f3c43d0839404/Traefik/docker-compose.yml)

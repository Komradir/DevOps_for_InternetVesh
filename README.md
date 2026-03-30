№1 Базовая подготовка операционной системы (актульно на Debian 13):
  1.1. установка утилиты sudo (выполняется из под root):
    apt install sudo -y
  1.2. дать пользователю возможность выполнять команду sudo
    nano /etc/sudoers, добавить в файл строчку [user] ALL=(ALL:ALL) ALL
  1.3 апдейт репозиториев и установка базового ПО:
    sudo apt update && sudo apt upgrade -y && sudo apt install -y mc ufw git htop curl ca-certificates
  1.4 установка docker ( и сопутствующего ПО) и его проверка
    sudo apt install docker.io
    sudo systemctl status docker
    sudo docker run hello-world

№2. создание и настройка кластера docker swarm
  2.1. Инициализация нодый swarm
    sudo docker swam init --advertise-addr [ip адресс к которому будут обращатся другие ноды. параметр обязателен,мы не может не сказать его, не смотря на то что планируется всего одна нода]
  2.2. загрузка файла монифеста swarm, конфиги postgresql и pgAdmin с данного репозитория ditgub. Разбор содержимого выполнен анутри самих файлов по средствам копентариев.
    wget -L https://raw.githubusercontent.com/Komradir/DevOps_for_InternetVesh/refs/heads/main/swarm-stack.yml
    wget -L https://raw.githubusercontent.com/Komradir/DevOps_for_InternetVesh/refs/heads/main/servers.json
    wget -L https://github.com/Komradir/DevOps_for_InternetVesh/tree/main/pg_confs/
  2.3. Деплой стека swarm 
     sudo docker stack deploy -c swarm-stack.yml DevOps 
     
Основные недочеты на данный момент:
 1) Ошибка инициализации базы данных postgresql. Ошибка database "DataBas" does not exist.

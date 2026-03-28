№1 Базовая подготовка операционной системы (актульно на Debian 13):
  1.1. установка утилиты sudo (выполняется из под root):
    apt install sudo -y
  1.2. дать пользователю возможность выполнять команду sudo
    nano /etc/sudoers, добавить в файл строчку [user] ALL=(ALL:ALL) ALL
  1.3 апдейт репозиториев и установка базового ПО:
    sudo apt update && sudo apt upgrade -y && sudo apt install -y mc ufw git htop curl ca-certificates
  1.4.создание директории для GPG-key (он потрубуется добавления дополнительных репизиториев)
    sudo install -m 0755 -d /etc/apt/keyrings  
  1.5 добавление GPG-key от официального репозитория doker
    sudo curl -fSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc    
  1.6 добавление права на чтание GPG-ключа doker (т.к. это ключ от официального репозитория docker возможноть чтения для всех пользователей не должна привестик проблемам) 
    sudo chmod a+r /etc/apt/keyrings/docker.asc
  1.7 добавление офф репозитория docker в список (команды с офф документации)
    sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
    Types: deb
    URIs: https://download.docker.com/linux/debian
    Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
    Components: stable
    Architectures: $(dpkg --print-architecture)
    Signed-By: /etc/apt/keyrings/docker.asc
    EOF

    sudo apt update

  1.8 установка docker ( и сопутствующего ПО) и его проверка
    sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    sudo systemctl status docker
    sudo docker run hello-world

№2. создание и настройка кластера docker swarm
  2.1. Инициализация нодый swarm
    sudo docker swam init --advertise-addr [ip адресс к которому будут обращатся другие ноды. параметр обязателен,мы не может не сказать его, не смотря на то что планируется всего одна нода]
  2.2. загрузка файла монифеста swarm с данного репозитория ditgub
    wget -L https://github.com/Komradir/DevOps_for_InternetVesh/swarm-stack.yml
  


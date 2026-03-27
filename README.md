№1 Базовая подготовка операционной системы (актульно на Debian 13):
  1.1. установка утилиты sudo (выполняется из под root):
    apt install sudo -y
  1.2. дать пользователю возможность выполнять команду sudo
    nano /etc/sudoers, добавить в файл строчку [user] ALL=(ALL:ALL) ALL
  1.3 апдейт репозиториев и установка базового ПО:
    sudo apt update && sudo apt upgrade -y && sudo apt install -y mc ufw git htop curl 

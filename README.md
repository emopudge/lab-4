# Лабораторная работа 4
## Цель 

## Задание:

1. Запуск aafire в контейнере:

a. Создание Dockerfile:

dockerfile

FROM ubuntu:latest

RUN apt-get update && apt-get install -y aafire ping

CMD ["aafire"]

b. Построение образа:

Bash

sudo docker build . -t aafire-container . 

c. Запуск контейнера:

Bash

docker run -d -it aafire-container

d. Скриншот:

!aafire-container

2. Настройка сети между двумя контейнерами:

a. Создание сети:

Bash

docker network create myNetwork

b. Запуск двух контейнеров:

Bash

docker run -d -it --network myNetwork aafire-container 
docker run -d -it --network myNetwork aafire-container

c. Получение ID контейнеров:

Bash

docker ps

d. Подключение контейнеров к сети:

Bash

docker network connect myNetwork <container_id_1>
docker network connect myNetwork <container_id_2>

e. Проверка настроек сети:

Bash

docker network inspect myNetwork

f. Тестирование соединения:

Bash

docker exec -it <container_id_1> ping <container_id_2>

g. Скриншот:

!ping-containers

Объяснения:

 Dockerfile: В этом файле мы используем образ Ubuntu, устанавливаем приложение `aafire` и утилиту `ping` и запускаем `aafire` как команду.
 docker build: Строим образ Docker с именем aafire-container из Dockerfile.
 docker run: Запускаем контейнер в фоновом режиме (`-d`) с интерактивной оболочкой (`-it`) и подключаем его к сети `myNetwork`.
 docker network create: Создаем новую сеть с именем myNetwork.
 docker ps: Получаем список запущенных контейнеров.
 docker network connect: Подключаем контейнеры к сети myNetwork.
 docker network inspect: Проверяем настройки сети.
 docker exec: Запускаем команду ping в контейнере container_id_1, чтобы проверить соединение с контейнером container_id_2.

Результат:

Теперь два контейнера подключены к общей сети myNetwork, и вы можете проверить соединение между ними с помощью ping.

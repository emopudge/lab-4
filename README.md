# Лабораторная работа 4
## Цель 

## Задание:

sudo apt install libaa-bin


sudo docker ps -a - посмотреть все созданные контейнеры
sudo docker images - посмотреть все образы в докер

1. Запуск aafire в контейнере:

a. Создание Dockerfile:

dockerfile

FROM ubuntu:latest

RUN apt-get update && sudo apt-get install -y inetutils-ping

CMD ["aafire"]

b. Построение образа:

Bash

sudo docker build . -t aafire 

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









# Отчет по лабораторной работе: Настройка сети между контейнерами

## Цель работы:  
Запустить приложение "aafire" в Docker-контейнерах, настроить сеть между двумя контейнерами и протестировать соединение с использованием утилиты ping.

## Шаги выполнения:

1. **Установка библиотеки libaa-bin**
```bash
sudo apt install libaa-bin
```
2. **Созлание dockerfile**
   ```bash
   FROM ubuntu:latest

   RUN apt-get update && apt-get install -y libaa-bin inetutils-ping && apt-get clean && rm -rf /var/lib/apt/lists/*

   CMD ["aafire"]

   ```
3. **Построение образа**
   ```bash
   
   ```
5. **Создание сети между контейнерами**

   Затем создаём сеть с именем "myNetwork":
```bash
   bash
   docker network create myNetwork
```   
4. **Подключение контейнеров к созданной сети**

   Подключаем оба контейнера к только что созданной сети:
```bash
   bash
   docker network connect myNetwork mycontainer1
   docker network connect myNetwork mycontainer2
  ``` 
5. **Проверка настроек сети**

   Для проверки настроек сети выполняем команду:
```bash
   bash
   docker network inspect myNetwork
```   
   Это позволит увидеть, что оба контейнера подключены к сети.

6. **Тестирование соединения между контейнерами**

   Открываем новое окно терминала и проверяем соединение между контейнерами с помощью утилиты ping:
```bash
   bash
   docker exec -it mycontainer1 ping mycontainer2
 ```  
   **Скриншот тестирования соединения:**
   
   ![Скриншот тестирования соединения](ссылка_на_скриншот)

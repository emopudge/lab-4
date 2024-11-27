
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
3. **Построение образа (image)**
   ```bash
   sudo docker build . -t my-aafire 
   ```
4. **Создание контейнеров**
   ```
   sudo docker run -it --name my-aafire-1 my-aafire
   sudo docker run -it --name my-aafire-2 my-aafire
   ```
4.5. **Повторный запуск контейнеров с этими именами**
   ```
   sudo docker start my-aafire-1
   ```
затем, если хотим увидеть огонь:
   ```
   sudo docker exec -it my-aafire-1 aafire
   ```
5. **Создание сети между контейнерами**
```bash
   docker network create myNetwork
```   
6. **Подключение контейнеров к созданной сети**

   Подключаем оба контейнера к только что созданной сети:
```bash
   bash
   docker network connect myNetwork my-aafire-1
   docker network connect myNetwork my-aafire-2
  ``` 
7. **Тестирование соединения между контейнерами**

   Открываем новое окно терминала и проверяем соединение между контейнерами с помощью утилиты ping:
```bash
   bash
   docker exec -it my-aafire-1 ping my-aafire-2
 ```  
   **Скриншот тестирования соединения:**
   

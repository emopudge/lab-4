









# Отчет по лабораторной работе: Настройка сети между контейнерами

## Цель работы:  
Запустить приложение "aafire" в Docker-контейнерах, настроить сеть между двумя контейнерами и протестировать соединение с использованием утилиты ping.

## Шаги выполнения:

1. **Созлание dockerfile**
   ```bash
   FROM ubuntu:latest

   RUN apt-get update && apt-get install -y libaa-bin inetutils-ping && apt-get clean && rm -rf /var/lib/apt/lists/*

   CMD ["aafire"]

   ```
2. **Построение образа (image)**
   ```bash
   sudo docker build . -t my-aafire 
   ```
3. **Создание контейнеров**
   ```
   sudo docker run -it --name my-aafire-1 my-aafire
   sudo docker run -it --name my-aafire-2 my-aafire
   ```
   ![image](https://github.com/user-attachments/assets/00e0e1b6-0e5d-45f2-8a08-9f50552babaf)

3.5. **Повторный запуск контейнеров с этими именами**
   ```
   sudo docker start my-aafire-1
   ```
затем, если хотим увидеть огонь:
   ```
   sudo docker exec -it my-aafire-1 aafire
   ```
4. **Создание сети между контейнерами**
```bash
   docker network create myNetwork
```   
5. **Подключение контейнеров к созданной сети**

   Подключаем оба контейнера к только что созданной сети:
```bash
   docker network connect myNetwork my-aafire-1
   docker network connect myNetwork my-aafire-2
  ``` 
6. **Тестирование соединения между контейнерами**

   Открываем новое окно терминала и проверяем соединение между контейнерами с помощью утилиты ping:
```bash
   docker exec -it my-aafire-1 ping my-aafire-2
 ```  
![image](https://github.com/user-attachments/assets/de3c7604-51b6-49aa-8287-9500cdfa2a5d)
   

![image](https://github.com/user-attachments/assets/36fa924a-f81b-49a2-bf51-627e10df4c0b)

[Download](https://kafka.apache.org/downloads) - ```tar -xzf ...```

Все основные скрипты в ```/bin/```

Генерируем ID для kafka кластера: ```./bin/kafka-storage.sh random-uuid```

---

F-60G3BZR7eptWXNUux9pQ

---

Форматируем логи для совместимости с kraft режимом

```./bin/kafka-storage.sh format -t F-60G3BZR7eptWXNUux9pQ -c config/kraft/server.properties```

Выдаст что-то тип такого

![image](https://github.com/user-attachments/assets/a534ffd2-5d1b-44b7-afc2-53d242bfd729)

Запускаем кафку для теста пока что с дефолтным конфигом ```./bin/kafka-server-start.sh config/kraft/server.properties```

Для локального кластера дублируем server.properties в server-1.properties, server-2.properties и server-3.properties, и меняем:
 - node.id - уникальный идентификатор для сервера Kafka в кластере 
   - node.id=1 для 1ого, node.id=2 для 2ого и node.td=3 для 3его
 - listeners - список адресов (host:port) для брокеров и контроллеров. Это сетевые интерфейсы, которые кафка использует для общения с другими серверами и клиентами
   - listeners=PLAINTEXT://:9092,CONTROLLER://:9093 ( то есть БРОКЕР будет слушать клиентов на 9092 порту, а КОНТРОЛЛЕР на 9093, эт для 1ого) , PLAINTEXT://:9094,CONTROLLER://:9095 для 2ого, PLAINTEXT://:9096,CONTROLLER://:9097 для 3его
 - contoller.quorum.voters - список избирателей, которые составляют кворум в кластере, принимая решения по обеспечению согласованности данных и отказоустойчивости
   - controller.quorum.voters=1@localhost:9093,2@localhost:9095,3@localhost:9097 ( 1 это node.id, localhost:9093 это CONTROLLER:9093 из listeners выше ) и далее 2 и 3 ноды, во всех 3х пишем одно и тож
 - advertised.listeners - список адресов для соединения с брокером, отличается от свойства "listeners", которое определяет адреса и порты, которые брокер Кафка использует для прослушивания входящих подключений ( то есть может быть прокси, какой-то список адресов, а в listeners указывается типо внутренний адрес)
   - advertised.listeners=PLAINTEXT://localhost:9092, указывается только БРОКЕР, PLAINTEXT://localhost:9094 для 2, PLAINTEXT://localhost:9096 для 3
 - log.dirs - локальная директория метаданных, логов, снапшотов данного сервера
   - log.dirs=/tmp/server-1/kraft-combined-logs 1ый, log.dirs=/tmp/server-2/kraft-combined-logs 2ой, log.dirs=/tmp/server-3/kraft-combined-logs 3ий
  
Так же форматируем логи для kraft у server-2 и server-3, как делали выше для server-1

Ну и запускаем ```./bin/kafka-server-start.sh config/kraft/server-1.properties``` 2ой и 3ий

Завершить можно по-дебильному через Ctrl + C, потеря логов, некорретное завершение итд, либо по-нормальному ```./bin/kafka-server-stop.sh```

## Создание топиков и партиций
кол-во consumers не может превышать кол-во партиций, 3 копии(1 в лидере, 2 в репликах, не может быть больше чем серверов), bootstap-server это список БРОКЕРОВ в кластере,можно 1 кэш указать, но лучше больше для надежности
```
./kafka-topics.sh --create --topic payment-created-events-topic --partitions 3 --replication-factor 3 --bootstrap-server localhost:9092,localhost:9094
```

```./kafka-topics.sh --list --bootstrap-server localhost:9092,localhost:9094``` список всех топиков

```./kafka-topics.sh --describe --bootstrap-server localhost:9092,localhost:9094``` детальная инфа о топиках

![image](https://github.com/user-attachments/assets/ffcebd71-e2ee-4000-87e7-4a2f204f1f53)

сами сообщения сохраняются в ЛОГАХ, а ЛОГИ делятся на СЕГМЕНТЫ

```./kafka-topics.sh --delete --topic payment-created-events-topic --bootstrap-server localhost:9092``` удаление топика

если вдруг всё сломалось, и нужно как-то радикально починить всё - можно удалить логи к херам) ```log.dirs=/tmp/server-1/kraft-combined-logs```

Пишем сообщение ```./kafka-console-producer.sh --topic payment-canceled-events-topic --bootstrap-server localhost:9092``` прям в терминале "Ключ-Значение" ( если топика нет - кафка наругается, но один фиг создаст его )

И читаем ```./kafka-console-consumer.sh --topic payment-canceled-events-topic --from-beginning --bootstrap-server localhost:9092```

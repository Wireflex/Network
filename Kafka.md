![image](https://github.com/user-attachments/assets/36fa924a-f81b-49a2-bf51-627e10df4c0b)

В директории кафки:

./bin/kafka-storage.sh random-uuid

HnWJ2SS4TN2yszSbPvc4_g
---
./bin/kafka-storage.sh format -t HnWJ2SS4TN2yszSbPvc4_g -c config/kraft/server-1.properties

./bin/kafka-server-start.sh config/kraft/server-1.properties

./kafka-topics.sh --create --topic payment-created-events-topic --partitions 3 --replication-factor 3 --bootstrap-server localhost:9092,localhost:9094

./kafka-topics.sh --list --bootstrap-server localhost:9092,localhost:9094

./kafka-topics.sh --describe --bootstrap-server localhost:9092,localhost:9094

./bin/kafka-server-stop.sh

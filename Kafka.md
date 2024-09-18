![image](https://github.com/user-attachments/assets/17326584-2f4c-4fb8-85f1-6d4ab6098b53)

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

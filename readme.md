# Certified Confluent Developer for Apache Kafka

Use [this guide](https://docs.confluent.io/platform/current/quickstart/ce-docker-quickstart.html) for local set up using docker.

Use the community edition docker version of the quick start.

Note: exam covers the confluent version of kafka.

Kafka generally requires no more than 6GB of heap space - significantly more or less than that is probably not a good configuration.

## Misc

### Command Line

To run commands via docker, change this:

```
./bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

To this:

```
docker-compose exec broker kafka-topics --list --bootstrap-server localhost:9092 
```

See partition and replica details:

```
docker-compose exec broker kafka-topics --bootstrap-server localhost:9092 --describe --topic default_ksql_processing_log
```

### Topic Lab

```
$ kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 3 --partitions 6 --topic inventory_purchases

$ kafka-console-producer --broker-list localhost:9092 --topic inventory_purchases
>product: apples, quantity: 5
>product: lemons, quantity: 7

$ kafka-topics --bootstrap-server localhost:9092 --describe --topic inventory_purchases
Topic:inventory_purchases       PartitionCount:6        ReplicationFactor:3     Configs:segment.bytes=1073741824
        Topic: inventory_purchases      Partition: 0    Leader: 2       Replicas: 2,3,1 Isr: 2,3,1
        Topic: inventory_purchases      Partition: 1    Leader: 3       Replicas: 3,1,2 Isr: 3,1,2
        Topic: inventory_purchases      Partition: 2    Leader: 1       Replicas: 1,2,3 Isr: 1,2,3
        Topic: inventory_purchases      Partition: 3    Leader: 2       Replicas: 2,1,3 Isr: 2,1,3
        Topic: inventory_purchases      Partition: 4    Leader: 3       Replicas: 3,2,1 Isr: 3,2,1
        Topic: inventory_purchases      Partition: 5    Leader: 1       Replicas: 1,3,2 Isr: 1,3,2

$ kafka-console-consumer --bootstrap-server localhost:9092 --topic inventory_purchases --from-beginning
product: apples, quantity: 5
product: lemons, quantity: 7
```

### Consumer Groups Labs

Single consumer

```
kafka-console-consumer --bootstrap-server localhost:9092 --topic inventory_purchases --group 1
```


Multiple consumers - multiple consumers work together to process all the messages one time between the both of them

```
kafka-console-consumer --bootstrap-server localhost:9092 --topic inventory_purchases --group 2 > /home/cloud_user/output/group2_consumer1.txt

kafka-console-consumer --bootstrap-server localhost:9092 --topic inventory_purchases --group 2 > /home/cloud_user/output/group2_consumer2.txt
```
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
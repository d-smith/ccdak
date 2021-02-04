

## Streams

```
$ docker-compose exec broker kafka-console-producer --broker-list localhost:9092 --topic streams-input-topic --property parse.key=true --property key.separator=:
>hello:jerkface


$ docker-compose exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic streams-output-topic --property print.key=true
hello	jerkface
```

## Joins

```
docker-compose exec broker kafka-console-producer --broker-list localhost:9092 --topic joins-input-topic-left --property parse.key=true --property key.separator=:

docker-compose exec broker kafka-console-producer --broker-list localhost:9092 --topic joins-input-topic-right --property parse.key=true --property key.separator=:

./gradlew runJoins

docker-compose exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic inner-join-output-topic --property print.key=true

docker-compose exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic left-join-output-topic --property print.key=true

docker-compose exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic outer-join-output-topic --property print.key=true
```
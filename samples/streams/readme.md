


```
$ docker-compose exec broker kafka-console-producer --broker-list localhost:9092 --topic streams-input-topic --property parse.key=true --property key.separator=:
>hello:jerkface


$ docker-compose exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic streams-output-topic --property print.key=true
hello	jerkface
```
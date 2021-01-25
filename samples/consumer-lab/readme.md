See https://github.com/linuxacademy/content-ccdak-kafka-simple-consumer

* Add kafka-client dependency to build.gradle (kafka-client:2.2.1)

Main looks like:

```
package com.linuxacademy.ccdak.kafkaSimpleConsumer;

import java.util.Properties;
import java.util.Arrays;
import org.apache.kafka.clients.consumer.*;
import java.time.Duration;

public class Main {

    public static void main(String[] args) {
        Properties props = new Properties();
        props.setProperty("bootstrap.servers", "localhost:9092");
        props.setProperty("group.id", "test");
             props.setProperty("enable.auto.commit", "true");
             props.setProperty("auto.commit.interval.ms", "1000");
             props.setProperty("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
                  props.setProperty("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        consumer.subscribe(Arrays.asList("inventory_purchases"));
        while(true) {

                ConsumerRecords<String,String> records = consumer.poll(Duration.ofMillis(100));
                for(ConsumerRecord<String,String> record: records) {

                        System.out.printf("offset = %d, key = %s, value = %s\n",record.offset(),record.key(), record.value());
                }
        }
    }

}
```
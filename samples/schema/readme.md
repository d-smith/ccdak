From here - git clone https://github.com/linuxacademy/content-ccdak-schema-registry.git

Gradle plugin to support object generation from avro schemas

id 'com.commercehub.gradle.plugin.avro' version '0.9.1'

Need confluent maven repository

maven { url 'https://packages.confluent.io/maven' }

And dependencies...

docker-compose exec broker kafka-topics --bootstrap-server localhost:9092 --create --topic employees --partitions 1 --replication-factor 1



docker-compose exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic employees --from-beginning
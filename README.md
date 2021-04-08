# kogito-travel-agency project

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## Running the application in dev mode

### Prerequisites
Infinispan & Kafka
```
docker-compose up -d
docker-compose down
```

Add cluster to Kafka Manager
```
curl localhost:9000/clusters --data "name=default&zkHosts=zookeeper:2181&kafkaVersion=0.8.2.1&jmxEnabled=true&jmxUser=&jmxPass=&pollConsumers=true&activeOffsetCacheEnabled=true&tuning.brokerViewUpdatePeriodSeconds=30&tuning.clusterManagerThreadPoolSize=2&tuning.clusterManagerThreadPoolQueueSize=100&tuning.kafkaCommandThreadPoolSize=2&tuning.kafkaCommandThreadPoolQueueSize=100&tuning.logkafkaCommandThreadPoolSize=2&tuning.logkafkaCommandThreadPoolQueueSize=100&tuning.logkafkaUpdatePeriodSeconds=30&tuning.partitionOffsetCacheTimeoutSecs=5&tuning.brokerViewThreadPoolSize=4&tuning.brokerViewThreadPoolQueueSize=1000&tuning.offsetCacheThreadPoolSize=4&tuning.offsetCacheThreadPoolQueueSize=1000&tuning.kafkaAdminClientThreadPoolSize=4&tuning.kafkaAdminClientThreadPoolQueueSize=1000&tuning.kafkaManagedOffsetMetadataCheckMillis=30000&tuning.kafkaManagedOffsetGroupCacheSize=1000000&tuning.kafkaManagedOffsetGroupExpireDays=7&securityProtocol=PLAINTEXT&saslMechanism=DEFAULT" -X POST
```

Kafka Topics
* visaapplications - used to send visa application that are consumed and processed by Kogito Visas service
* kogito-processinstances-events - used to emit events by kogito that can be consumed by data index service and other services
* kogito-usertaskinstances-events -used to emit events by kogito that can be consumed by data index service



### App
You can run your application in dev mode that enables live coding using. Run this command in each of the modules:
```
./mvnw quarkus:dev
```

or
```
mvn clean compile quarkus:dev
```

Access app at http://localhost:8080 and metrics at http://localhost:8080/metric

## Running unit tests

```
mvn verify
```

## Inspecting Kafka
how to:
```
docker exec -it 8ff91b27aa98 /bin/bash
cd /bin
kafka-console-consumer --bootstrap-server localhost:9092 --topic kogito-processinstances-events --from-beginning
```
## Packaging and running the application

The application can be packaged using `./mvnw package`.
It produces the `kogito-travel-agency-1.0-SNAPSHOT-runner.jar` file in the `/target` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/lib` directory.

The application is now runnable using `java -jar target/kogito-travel-agency-1.0-SNAPSHOT-runner.jar`.

## Creating a native executable

You can create a native executable using: `./mvnw package -Pnative`.

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: `./mvnw package -Pnative -Dquarkus.native.container-build=true`.

You can then execute your native executable with: `./target/kogito-travel-agency-1.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/building-native-image-guide.

## Referenced Blog
https://sgitario.github.io/kogito-travel-agency-example/

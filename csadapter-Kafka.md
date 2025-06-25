## Csadapter 관점에서 Kafka 연동 설명

**Csadapter 개요**

Csadapter는 Kafka와의 통합을 위한 어댑터로, Kafka 메시징 시스템과의 연결을 통해 메시지를 송수신할 수 있는 기능을 제공합니다. 이 어댑터는 Kafka의 퍼블리시-구독 모델을 활용하여 다양한 애플리케이션 간의 데이터 흐름을 관리합니다.

### Kafka Producer 구현

Kafka Producer는 메시지를 Kafka 토픽에 전송하는 역할을 합니다. 아래는 Csadapter를 활용하여 Kafka Producer를 구현하는 예제입니다.

```java
public class KafkaProducerExample {
    private static final Logger log = LoggerFactory.getLogger(KafkaProducerExample.class.getSimpleName());

    public static void main(String[] args) {
        Properties properties = new Properties();
        properties.setProperty(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "127.0.0.1:9092");
        properties.setProperty(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
        properties.setProperty(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);
        String topic = "demo_topic";

        for (int i = 0; i < 10; i++) {
            String key = "key_" + i;
            String value = "message_" + i;

            ProducerRecord<String, String> record = new ProducerRecord<>(topic, key, value);
            producer.send(record, (metadata, exception) -> {
                if (exception == null) {
                    log.info("Sent message with key: {} to partition: {}", key, metadata.partition());
                } else {
                    log.error("Error sending message", exception);
                }
            });
        }

        producer.flush();
        producer.close();
    }
}
```

**코드 설명**:
- `Properties` 객체를 통해 Kafka 브로커의 주소와 직렬화 방식을 설정합니다.
- `KafkaProducer` 객체를 생성하고, `ProducerRecord`를 통해 메시지를 구성합니다.
- `send` 메서드를 호출하여 메시지를 비동기적으로 전송하며, 전송 결과를 콜백으로 처리합니다.

### Kafka Consumer 구현

Kafka Consumer는 Kafka 토픽에서 메시지를 수신하는 역할을 합니다. 아래는 Csadapter를 활용하여 Kafka Consumer를 구현하는 예제입니다.

```java
public class KafkaConsumerExample {
    private static final Logger log = LoggerFactory.getLogger(KafkaConsumerExample.class.getSimpleName());

    public static void main(String[] args) {
        String groupId = "my-java-application";
        String topic = "demo_topic";

        Properties properties = new Properties();
        properties.setProperty("bootstrap.servers", "127.0.0.1:9092");
        properties.setProperty("key.deserializer", StringDeserializer.class.getName());
        properties.setProperty("value.deserializer", StringDeserializer.class.getName());
        properties.setProperty("group.id", groupId);
        properties.setProperty("auto.offset.reset", "earliest");

        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(properties);
        consumer.subscribe(Arrays.asList(topic));

        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(1000));
            for (ConsumerRecord<String, String> record : records) {
                log.info("Received message with key: {} and value: {}", record.key(), record.value());
            }
        }
    }
}
```

**코드 설명**:
- `Properties` 객체를 사용하여 Kafka 브로커의 주소와 역직렬화 방식을 설정합니다.
- `KafkaConsumer` 객체를 생성하고, `subscribe` 메서드를 통해 구독할 토픽을 설정합니다.
- `poll` 메서드를 사용하여 주기적으로 메시지를 가져오고, 수신된 메시지를 로그로 출력합니다.

### 결론

Csadapter를 통해 Kafka와의 통합을 구현하면, 애플리케이션 간의 데이터 흐름을 효율적으로 관리할 수 있습니다. 위의 Producer와 Consumer 예제 코드를 통해 Kafka의 메시징 기능을 활용하여 실시간 데이터 처리 및 이벤트 기반 아키텍처를 구축할 수 있습니다. 이러한 통합은 다양한 비즈니스 요구 사항을 충족하는 데 유용하게 활용될 수 있습니다.
[1] https://help.sap.com/docs/cloud-integration/sap-cloud-integration/kafka-adapter
[2] https://help.sap.com/docs/cloud-integration/sap-cloud-integration/configure-kafka-receiver-adapter
[3] https://min9yu98.tistory.com/24
[4] https://velog.io/@luna_lee/Apache-Kafka-4-JAVA%EC%99%80-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0Producer-Consumer
[5] https://m.blog.naver.com/fbfbf1/223101198904
[6] http://thefarmersfront.github.io/blog/kafka-connect-pipeline/
[7] https://stackoverflow.com/questions/51631900/creating-a-message-driven-inbound-channel-adapter-to-connect-to-kafka-using-spri
[8] https://docs.webmethods.io/on-premises/webmethods-adapter-for-apache-kafka/en/9.6.0/webhelp/kafka-webhelp/ta-install.html
[9] https://documentation.sas.com/doc/en/espca/4.2/p0sbfix2ql9xpln1l1x4t9017aql.htm
[10] https://github.com/spring-projects/spring-integration-samples/blob/master/basic/kafka/README.md
[11] https://medium.com/@seohee.sophie.kwon/kafka-consumer-%EB%A7%8C%EB%93%A4%EA%B8%B0-8b6638a46750
[12] https://www.kai-waehner.de/blog/2020/08/25/kafka-sap-integration-alternatives-connectors-erp-r3-ecc-s4-hana-soap-rest-http-web-service-api-sdk-java/
[13] https://documentation.sas.com/doc/en/espca/6.2/p0sbfix2ql9xpln1l1x4t9017aql.htm
[14] https://docs.confluent.io/platform/current/connect/index.html
[15] https://dkswnkk.tistory.com/705
[16] https://github.com/mikezaschka/cds-kafka
[17] https://cjw-awdsd.tistory.com/53
[18] https://www.couchbase.com/blog/ko/getting-started-with-kafka-and-couchbase-as-an-endpoint/
[19] https://hyem207.tistory.com/76
[20] https://devel-repository.tistory.com/46
[21] https://medium.com/simform-engineering/kafka-integration-made-easy-with-spring-boot-b7aaf44d8889
[22] https://docs.spring.io/spring-integration/reference/kafka.html

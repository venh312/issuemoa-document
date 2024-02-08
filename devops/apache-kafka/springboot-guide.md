## 스프링 부트와 Spring Kafka를 사용하여 Kafka를 통해 발행 및 구독 예제

### build.gradle 파일에 Spring Kafka 라이브러리 추가
```
implementation 'org.springframework.kafka:spring-kafka'
```

그런 다음, 프로듀서와 컨슈머를 각각 구현합니다.

### Kafka 프로듀서

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Component;

@Component
public class KafkaProducer {

    private static final String TOPIC_NAME = "issuemoa-topic";

    @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    public void sendMessage(String message) {
        kafkaTemplate.send(TOPIC_NAME, message);
        System.out.println("Produced message: " + message);
    }
}
```


### Kafka 컨슈머
```java
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Component;

@Component
public class KafkaConsumer {

    private static final String TOPIC_NAME = "issuemoa-topic";

    @KafkaListener(topics = TOPIC_NAME, groupId = "group1")
    public void consumeMessage(String message) {
        System.out.println("Consumed message: " + message);
    }
}
```

이제 프로듀서에서 메시지를 발행하고 컨슈머에서 해당 메시지를 구독합니다.

예를 들어, 컨트롤러에서 프로듀서를 주입하고 메시지를 발행하는 메서드를 추가할 수 있습니다.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class KafkaController {

    @Autowired
    private KafkaProducer kafkaProducer;

    @GetMapping("/publish/{message}")
    public String sendMessage(@PathVariable String message) {
        kafkaProducer.sendMessage(message);
        return "Message sent to Kafka: " + message;
    }
}
```

그리고 스프링 부트 애플리케이션을 실행하면, /publish/{message} 엔드포인트를 통해 메시지를 발행할 수 있습니다. 컨슈머는 해당 토픽을 구독하고 발행된 메시지를 수신하여 처리합니다.




## Kafka + Zookeeper 같이 사용되는 이유
`Kafka`는 분산 메시징 시스템으로서, 데이터를 안정적으로 처리하고 저장하기 위한 목적으로 사용됩니다. 그러나 `Kafka` 자체만으로는 분산 시스템을 구축하기에는 충분하지 않습니다. `Kafka`는 자체적으로 분산된 브로커들의 클러스터를 형성할 수 있지만, 클러스터 내의 브로커들 간에 상태 정보를 공유하고 관리하기 위해 외부 도구가 필요합니다.

`Zookeeper`는 이러한 목적으로 사용됩니다. `Zookeeper`는 분산 시스템에서의 동기화, 설정 관리, 리더 선출 등의 기능을 제공하여 `Kafka` 클러스터의 안정성과 일관성을 유지합니다. `Zookeeper`를 사용하면 `Kafka` 클러스터 내의 브로커들이 서로 통신하고 상태 정보를 공유하여 안정적으로 운영될 수 있습니다.

따라서 `Kafka`는 `Zookeeper`와 함께 사용되어야 하며, `Kafka` 클러스터를 구성하는 데 필수적인 역할을 합니다. `Zookeeper`를 사용하여 `Kafka` 클러스터를 관리하고 모니터링함으로써 안정적이고 신뢰할 수 있는 분산 시스템을 구축할 수 있습니다.


## docker-compose 실행
```
docker-compose -f issuemoa-kafka-docker-compose.yml up -d
```
- -f: 명시적으로 파일을 지정(default: docker-compose.yml)
- -d: 백그라운드 모드로 실행

## environment 옵션
#### KAFKA_CREATE_TOPICS
`issuemoa-topic` 이름의 토픽을 생성하고, 이 토픽은 1개의 파티션과 복제 팩터로 1을 갖는다는 것을 의미합니다. 
만약 다수의 토픽을 생성하려면 각 토픽을 쉼표로 구분하여 나열하면 됩니다.

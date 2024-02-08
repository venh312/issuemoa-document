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

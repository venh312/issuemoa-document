## Logstash
Logstash는 플러그인 기반의 데이터 수집 및 처리 엔진으로서, 광범위한 플러그인이 구비되어 다양한 수많은 아키텍처에서 손쉽게 데이터를 수집, 처리, 전달할 수 있게 해줍니다.

프로세싱은 하나 이상의 파이프라인으로 구성됩니다. 각 파이프라인에서 하나 이상의 입력 플러그인이 내부 대기열에 배치된 데이터를 수신하거나 수집합니다. 이것은 기본적으로 작고 메모리에 보관되지만 안정성과 복원력을 향상시키도록 디스크에서 더 크고 영구적으로 구성할 수 있습니다.

![image](https://github.com/conf312/issuemoa-document/assets/13326651/ae17fec9-a358-45c9-9d98-a68bc86255a5)

프로세싱 스레드는 대기열에서 데이터를 마이크로 배치로 읽은 다음, 구성된 필터 플러그인을 통해 순서대로 처리합니다. Logstash는 기본으로 특정 유형의 처리를 목표로 하는 많은 수의 플러그인과 함께 제공되며, 이렇게 해서 데이터가 구문 분석, 처리 및 강화됩니다.

데이터가 처리되면 프로세싱 스레드는 데이터를 포맷하고 Elasticsearch에 전송을 담당하는 적절한 출력 플러그인에 데이터를 전송합니다.

입력 및 출력 플러그인에서 codec 플러그인을 구성할 수도 있습니다. 이렇게 하면 데이터를 내부 대기열에 넣거나 출력 플러그인에 보내기 전에 데이터의 구문 분석 및/또는 포맷을 지정할 수 있습니다.


### install
```
sudo apt install apt-transport-https
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo sh -c 'echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/logstash-7.x.list'
sudo apt update
sudo apt install logstash
```

### logstash.conf 파일 생성
```
vi /etc/logstash/conf.d/logstash.conf
```

`pipeline.yml`에 path.config: `"/etc/logstash/conf.d/*.conf"`로 .conf 파일을 *로 설정 되어있어서 꼭 logstash 파일이름으로 .conf 파일을 생성하지 않아도 됩니다.
확장자는 지키기!

```
input {
  beats {
    port => 5044
    host => "0.0.0.0"
  }
}

output {
  elasticsearch {
    hosts => "[Elasticsearch IP]:9200"
    index => "logstash-%{+YYYY.MM.dd}"
  }
}}
```
beat로 부터 데이터를 `input` 받아 가공(filter) 후 `elasticsearch` 로 `ouput` 합니다.

크게는 input / filter / output 구조로 이어지는데 `fileter` 부분 설정을 생략하였습니다.

### Reference
- https://www.elastic.co/kr/blog/a-practical-introduction-to-logstash

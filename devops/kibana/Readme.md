## Kibana
kibana는 Elastic Stack 기반으로 구축된 오픈소스 프론트엔드 애플리케이션으로 Elasticsearch에서 색인된 데이터를 검색해서 분석 및 `시각화` 하는 기능 플랫폼입니다.

### install
```
sudo apt update
sudo apt install kibana
```

### 기본 설정
- [Kibana IP]:5601 로 접속 후 왼쪽 메뉴의 Discover를 선택합니다.
- logstash → logstash.conf 파일에 output 설정을 보면 `index => index => "logstash-%{+YYYY.MM.dd}"` 로 설정 되어 있습니다.
- elasticsearch는 이 index를 기반으로 생성하며, kibana에서 시각화 할 수 있습니다.
- logstash-날짜로 생성했기 때문에 discover 설정 index pattern 에 `logstash-*` 로 설정합니다.

<img width="549" alt="스크린샷 2024-02-09 오전 9 06 16" src="https://github.com/conf312/issuemoa-document/assets/13326651/a18db67c-53a6-4676-909b-57cb26dd9647">

<img width="1512" alt="스크린샷 2024-02-09 오전 9 11 32" src="https://github.com/conf312/issuemoa-document/assets/13326651/adb79ecb-f41d-42a8-8e3b-d477334c73cd">

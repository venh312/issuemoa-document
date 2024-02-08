## filebeat 
Filebeat는 Elastic Stack의 일부로, 로그 파일과 데이터를 수집하여 전송하는 경량 데이터 수집기입니다. 주로 로그 파일, 이벤트 로그 및 서버 및 애플리케이션에서 생성되는 다양한 형식의 데이터를 실시간으로 수집하여 Elastic Stack으로 전송합니다. 이러한 데이터는 Elasticsearch, Logstash 또는 Kibana와 같은 Elastic Stack의 다른 구성 요소에서 검색, 분석 및 시각화할 수 있습니다.

`filebeat.yml`의 inputs.paths(input)에 설정한 로그 파일 데이터를 수집하여 `logstash`(output)로 전송한다.
```
filebeat.inputs:
- type: log
  id: my-filestream-id
  enabled: true
  paths:
    - /home/venh/logs/*.log
```

### filebeat install
```
sudo apt install apt-transport-https
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo sh -c 'echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/logstash-7.x.list'
sudo apt update
sudo apt install logstash
```

### filebeat 로그 파일 생성
기본적으로 `/var/log` 경로에 filebeat 디렉토리가 생성되지 않을 경우 `filebeat.yml` 에 로깅 설정을 해준다.
```
vi /etc/filebeat/filebeat.yml
```

```
logging.level: info
logging.to_files: true
logging.files:
  path: /var/log/filebeat
  name: filebeat
  keepfiles: 7
  permissions: 0640
```

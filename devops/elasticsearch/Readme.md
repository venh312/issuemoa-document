## Elasticsearch Install
https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html

### Import the Elasticsearch PGP Key
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```

### Installing from the APT repository
```
sudo apt-get install apt-transport-https
```
```
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

### Elasticsearch Install
```
sudo apt-get update && sudo apt-get install elasticsearch
```

## 서비스 관리 및, 로그, 설치 경로

### 시작, 중지, 상태 확인, 재시작
```
systemctl start elasticsearch
systemctl stop elasticsearch
systemctl status elasticsearch
systemctl restart elasticsearch
```

### 실행 확인
```
curl localhost:9200
```
```
{
  "name" : "note-venh-ubuntu",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "BUhGTUZpTASpGq5mMut2zQ",
  "version" : {
    "number" : "8.12.1",
    "build_flavor" : "default",
    "build_type" : "deb",
    "build_hash" : "6185ba65d27469afabc9bc951cded6c17c21e3f3",
    "build_date" : "2024-02-01T13:07:13.727175297Z",
    "build_snapshot" : false,
    "lucene_version" : "9.9.2",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```

### elasticsearch.yml 경로
```
cd /etc/elasticsearch
```

### elasticsearch.log 경로
```
cd /var/log/elasticsearch
```

### 설치 후 9200 포트로 접근이 안 될 경우 로그 확인
`Received plaintext http traffic on an https channel, closing connection` 기본 SSL 적용으로 되어 있기 때문에 http 접근 시 아래 옵션을 `false`로 변경 후 재시작한다.
```
xpack.security.enabled: false
xpack.security.enrollment.enabled: false
xpack.security.http.ssl: enabled: false
xpack.security.transport.ssl: enabled: false
```




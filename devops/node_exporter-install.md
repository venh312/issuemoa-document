### Node Exporter 다운로드

공식 GitHub 릴리스 페이지에서 Node Exporter를 다운로드합니다.
```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
```

### 압축 해제
다운로드 받은 tar 파일을 압축 해제합니다.
```bash
tar xvfz node_exporter-1.7.0.linux-amd64.tar.gz
```

### 바이너리 파일 이동
압축 해제한 디렉토리로 이동하여 바이너리 파일을 원하는 위치로 이동시킵니다. 일반적으로 /usr/local/bin 디렉토리에 이동시킵니다.
```bash
sudo mv node_exporter-1.7.0.linux-amd64/node_exporter /usr/local/bin/
```

### Node Exporter 서비스 파일 생성
systemd를 사용하여 Node Exporter를 관리하기 위해 서비스 파일을 생성합니다.
```bash
sudo nano /etc/systemd/system/node_exporter.service
```

### 서비스 파일에 다음 내용을 추가합니다
```bash
[Unit]
Description=Node Exporter
After=network.target

[Service]
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=default.target
```

### Node Exporter 서비스 시작
Node Exporter 서비스를 시작하고 부팅 시 자동으로 시작하도록 설정합니다.
```bash
sudo systemctl start node_exporter
sudo systemctl enable node_exporter
```

### 접속
```
http://localhost:9100

// metrics
http://localhost:9100/metrics
```


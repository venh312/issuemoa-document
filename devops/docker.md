## 🧷 Docker 파이프라인
#### 도커 명령어
https://github.com/conf312/concept-description/blob/master/concept/Docker/command.md

## 🌈 네트워크 생성
```
docker network create issuemoa
```

## 🌈 MySQL
#### MySql 이미지 생성
```
docker pull mysql
```

#### MySQL 컨테이너 실행
```
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=패스워드 \
  -p 3306:3306 \
  -v /var/lib/mysql:/var/lib/mysql \
  mysql
```

#### MySQL 덤프 생성
```
mysqldump -u [계정] -p [데이터베이스명] > [/경로/파일명.sql]
```

#### MySQL 덤프 복원
```
mysql -u [계정] -p [데이터베이스명] < [/경로/파일명.sql]
```

## 🌈 MongoDB
#### MongoDB 이미지 생성
```
docker pull mongo
```
#### MongoDB 컨테이너 실행
```
docker run -d \
  --name mongo \
  -p 27017:27017 \
  -v /data/db:/data/db \
  mongo
```
사용자 계정 추가 후 컨테이너 실행 시 `--auth` 옵션 추가 (사용자 접근 권한 추가)

#### switched to db admin
```
use admin
```
#### create user
```
db.createUser({user: "root", pwd: "root", roles:["root"]})
```
#### connect root
```
mongo -u root -p root
```

## 🌈 Redis
#### Redis 이미지 생성
```
docker pull redis
```
#### Redis 컨테이너 실행
```
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis
```

## 🌈 Jenkins
#### Jenkins 이미지 생성
```
docker pull gpfm312/jenkins-jdk17
```

#### Jenkins 컨테이너 실행
```
docker run -d \
--name jenkins \
-p 9090:8080 \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /var/jenkins_home:/var/jenkins_home \
-u root \
-e TZ=Asia/Seoul \
jenkins/jdk17
```

## 🌈 Prometheus
#### Prometheus 이미지 생성
```
docker pull prom/prometheus
```

#### Prometheus 컨테이너 실행
-v: prometheus.yml 파일을 볼륨 마운트 경로에 위치 시켜야한다.    
-p: 기본 포트는 9090이지만, Jenkins가 9090으로 사용하고 있어서 9091로 변경한다.
```
docker run -d \
--name prometheus \
-p 9091:9090 \
-v /home/venh/prometheus.yml:/etc/prometheus/prometheus.yml \
prom/prometheus
```

## 🌈 Grafana
#### Grafana 이미지 생성
```
docker pull grafana/grafana
```

#### Grafana 컨테이너 실행
```
docker run -d --name grafana -p 3000:3000 grafana/grafana
```

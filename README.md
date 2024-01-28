## 🧷 Docker 파이프라인
### 도커 명령어
https://github.com/conf312/concept-description/blob/master/concept/Docker/command.md

## Initialization
### 네트워크 생성
```
docker network create issuemoa
```

### MySql 이미지 생성
```
docker pull mysql
```

### MySQL 컨테이너 실행
```
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=패스워드 \
  -p 3306:3306 \
  -v /var/lib/mysql:/var/lib/mysql \
  mysql
```

### MongoDB 이미지 생성
```
docker pull mongo
```
### MongoDB 컨테이너 실행
```
docker run -d \
  --name mongo \
  -p 27017:27017 \
  -v /data/db:/data/db \
  mongo
```

### Redis 이미지 생성
```
docker pull redis
```
### Redis 컨테이너 실행
```
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis
```

### Docker hub 에서 jenkins 도커 이미지 가져오기
```
docker pull gpfm312/jenkins-jdk17
```

### 컨테이너 실행
```
docker run --name jenkins -p 9090:8080 -p 50000:50000 -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/jenkins_home:/var/jenkins_home -u root jenkins/jdk17
```

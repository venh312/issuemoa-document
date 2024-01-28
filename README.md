## 🧷 Docker 파이프라인
#### 도커 명령어
https://github.com/conf312/concept-description/blob/master/concept/Docker/command.md

## 네트워크 생성
```
docker network create issuemoa
```

## MySQL
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

## MongoDB
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

## Redis
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

## Jenkins
#### Jenkins 이미지 생성
```
docker pull gpfm312/jenkins-jdk17
```

#### Jenkins 컨테이너 실행
```
docker run -d \
--name jenkins \
-p 9090:8080 -p 50000:50000 \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /var/jenkins_home:/var/jenkins_home \
-u root \
jenkins/jdk17
```

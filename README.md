## 🧷 Docker 파이프라인
### 도커 명령어
https://github.com/conf312/concept-description/blob/master/concept/Docker/command.md

## Initialization
### 네트워크 생성
```
docker network create issuemoa
```

### Docker hub 에서 jenkins 도커 이미지 가져오기
```
docker pull gpfm312/jenkins-jdk17
```

### 컨테이너 실행
```
docker run --name jenkins -p 9090:8080 -p 50000:50000 -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/jenkins_home:/var/jenkins_home -u root jenkins/jdk17
```

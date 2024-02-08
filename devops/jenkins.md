### 1. Docker hub 에서 jenkins 도커 이미지 가져오기
```
docker pull jenkins/jenkins:lts
```

### 2. 컨테이너 실행
```
docker run --name jenkins -p 9090:8080 -p 50000:50000 -d -v /var/run/docker.sock:/var/run/docker.sock -v 로컬 마운트 경로:/var/jenkins_home -u root jenkins/jdk17
```

### 3. 컨테이너 접속 후 도커 & 컴포즈 설치
```
docker exec -it jenkins /bin/bash
```
```
curl https://get.docker.com/ > dockerinstall && chmod 777 dockerinstall && ./dockerinstall
```
```
apt install docker-compose
```

### 4. GitHub Credentials 생성
#### Username with Password
- ID: Jenkins에서 사용할 식별자
- Username: 깃허브 아이디
- Password: 깃허브 토큰


### 5. 아이템 생성 후 파이프라인 작성
```
pipeline {
    agent any
    
    environment {
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Git Clone
                    git branch: "master", credentialsId: "conf-git", url: "https://github.com/conf312/issueMoa-board.git"
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    // 프로젝트 빌드 & jar 생성
                    sh "chmod 777 gradlew && ./gradlew bootJar"
                }
            }
        }
        stage('Dokcer Image Build') {
            steps {
                script {
                    // 도커 빌드 & 이미지 생성
                    sh "docker build -t issuemoa/board ."
                }
            }
        }
        stage('Dokcer Run Conatiner') {
            steps {
                script {
                    def containerRunning = sh(script: 'docker inspect -f \'{{.State.Running}}\' issuemoa-board 2>/dev/null', returnStatus: true) == 0
                    // 컨테이너가 이미 실행중이면 종료 및 삭제
                    if (containerRunning) {
                        echo 'Container is already running'
                        sh "docker stop issuemoa-board"
                        sh "docker rm issuemoa-board"
                    }
                    
                    sh "docker run -d --name issuemoa-board -p 17060:17060 --network issuemoa -e TZ=Asia/Seoul issuemoa/board"
                }
            }
        }
    }

    post {
        success {
            // 성공적으로 빌드된 경우 실행되는 작업
            echo 'Build successful!'

            // Git 커밋 메시지
            def commitMessage = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()

            // 슬랙 발송
            slackSend (
                channel: '#이슈모아', 
                color: '#0100FF', 
                message: "😄 이슈모아 Build & Release 성공! \n 💻 ${commitMessage} \n ${env.JOB_NAME},  buildNumber: [${env.BUILD_NUMBER}]"
            )

            // 이메일 발송
            def emailBody = """
                <html>
                <body>
                    <p>💻 상세정보:</p>
                    <ul>
                        <li>Commit: ${commitMessage}</li>
                        <li>Job: ${env.JOB_NAME}</li>
                        <li>Build Number: ${env.BUILD_NUMBER}</li>
                    </ul>
                </body>
            </html>
            """
            
            def recipients = ["conf312@naver.com", "gmlrb920@naver.com"]
            
            emailext(
                subject: "😄 이슈모아 프론트 & ${commitMessage}",
                body: emailBody,
                to: recipients.join(','),
                mimeType: "text/html"
            )
        }
        failure {
            // 빌드 실패한 경우 실행되는 작업
            echo 'Build failed!'
        }
    }
}
```

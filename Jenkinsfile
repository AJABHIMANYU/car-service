pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }

    stages {
        stage('Git') {
            steps {
                echo 'Pull code from GitHub'
                git url: 'https://github.com/AJABHIMANYU/car-service.git', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                echo 'Build project using Maven'
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                echo 'Test your application'
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy the project'
                bat 'docker rm -f car-sr || true'
                bat 'docker rmi -f car-service || true'
                bat 'docker build -t car-service .'
                bat 'docker run --network demoproject_app-network -p 8054:8054 -d --name car-sr car-service'
            }
        }
    }
}

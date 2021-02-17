pipeline {
    agent slave_kubemaster
    environment {
        PATH = "/opt/maven/apache-maven-3.6.3/bin:$PATH"
}
    stages {
        stage("git") {
            steps{
            git credentialsId: 'github_cred', url: 'https://github.com/anandsukan007/spring-boot-mongo-docker.git'
            }
        }
        stage("build code") {
            steps{
            sh "mvn clean package"
            }
        }
        stage('Build Docker Image'){
            //agent { label 'slave_kubemaster' }
        steps{
        sh 'docker build -t anandsukan007/spring-boot-mongo .'
    }
    }
    
    stage('Push Docker Image'){
    steps{
        withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'DOCKER_HUB_PASSWORD')]) {
              sh "docker login -u anandsukan007 -p ${DOCKER_HUB_PASSWORD}"
        }
        sh "docker push anandsukan007/spring-boot-mongo "
     }
     }
     }
     }

pipeline{
    agent any
    environment {
        registry = "gowthamsammangi/tensorgojava-app"
        registryCredential = 'dockerhub'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/GOWTHAMSAMMANGI/tensorgo-java-app.git'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                  dockerImage = docker.build registry + ":v$BUILD_NUMBER"
              }
            }
        }
        stage('Upload Image'){
          steps{
            script {
              docker.withRegistry('', registryCredential) {
                dockerImage.push("v$BUILD_NUMBER")
                dockerImage.push('latest')
              }
            }
          }
        }
        stage("TRIVY"){
            steps{
                sh "trivy image $registry + ":v$BUILD_NUMBER" > trivy.txt"
            }
        }
        stage('Deploy to container'){
            steps{
                sh "docker run -d --name fs-app -p 80:8070 $registry + ":v$BUILD_NUMBER""
            }
        }
    }
}
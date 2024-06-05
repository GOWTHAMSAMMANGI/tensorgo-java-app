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
        stage('Build docker image') {
            steps {
                sh "docker build -t image ."
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
                sh "trivy image $registry:v$BUILD_NUMBER > trivy.txt"
            }
        }
        stage('Deploy to container'){
            steps{
                sh "docker run -d --name fs-app -p 80:8070 $registry:v$BUILD_NUMBER"
            }
        }
    }
}
pipeline {
  environment {
    registry = "prasannakk/devops-certification"
    registryCredential = 'dockerhub'
  }
  agent any
  stages {
        stage('Building image') {
        steps{
            script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
        }
        }

        stage('Deploy Image') {
        steps{
            script {
            docker.withRegistry( '', 'dockerhub' ) {
                dockerImage.push()
            }
            }
        }
        }

        stage('Remove Image') {
        steps{
            sh "docker rmi $registry:$BUILD_NUMBER"
        }
        }
        stage('Execute Image'){
          steps{
            script {
              def customImage = docker.build("prasannakk/devops-certification:${env.BUILD_NUMBER}")
              customImage.inside {
                sh 'echo This is the code executing inside the container.'
              }
            }
          }
        }
   }   
}



pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') {
            agent{
                dockerfile{
                    filename 'Dockerfile'
                }
            steps { 
                script{
                 app = docker.build("Dockerfile")
                }
            }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('https://621617387058.dkr.ecr.ap-south-1.amazonaws.com/jenkins-demo', 'ecr:ap-south-1:5136f09d-bd27-412b-aa86-b4eee81f58df') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}

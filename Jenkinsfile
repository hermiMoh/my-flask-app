pipeline {
    agent any
    tools {
    }
    stages {
        stage("build image") {
            steps {
                echo 'building the docker image..'
                withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                    sh 'docker build -t medhermi/demo-app:flaskApp-1.0 .'
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push medhermi/demo-app:flaskApp-1.0'

                }
            }
        }
        stage("RUN Unit Tests") {
            steps {
                echo 'testing the application...'
                sh 'pip install -r requirements.txt'
                sh 'pytest tests/'
            }
        }
        stage("deploy") {
            steps {
                echo 'deploying the application...'
            }
        }
    }
    post {
        success {
            echo 'build and deploy successful..'
        }
        failure {
            echo 'pipeline failed.check logs..'
        }
    }
}
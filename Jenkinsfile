/bin/env groovy

pipeline {
    tools {
        maven 'Maven'
    }
    agent any
    stages {
        stage('build jar') {
            steps {
                script {
                    echo "Building the application..."
                    sh 'mvn package'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "Building the image..."
                    withCredentials([usernamePassword(credentialsID:'docker', passwordVariable:'PASS', usernameVariable: 'USER')]
                        sh 'docker build -t grprksh10/my-repo:jma-2.0 .'
                        sh "echo $PASS | dcoker login -u $USER --password-stdin"
                        sh 'docker push grprksh10/my-repo:jma-2.0'
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}

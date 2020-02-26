pipeline {
    agent any
    stages {
//         stage('Build') {
//             steps {
//                 echo 'Building...'
//                 sh './mvnw package'
//             }
//         }
        stage('Build Image') {
//             environment {
//                 DOCKER_HUB_PASS = credentials('docker-hub')
//             }
            steps {
                echo 'Build Image...'
                sh '''
                docker build -f Dockerfile -t kube:demo .
                '''
            }
        }
        stage('Create Deployment') {
            steps {
                echo 'Create Deployment ....'
                sh '''
                kubectl create deployment kube-demo --image=kube:demo
                '''
            }
        }
        stage('Create Service') {
            steps {
                echo 'Create Service ....'
                sh '''
                kubectl expose deployment kube-demo --type=LoadBalancer --port=8090
                '''
            }
        }
    }
}
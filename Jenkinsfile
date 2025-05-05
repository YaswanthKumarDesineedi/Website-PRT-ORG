pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dhubcred')
        DOCKER_BUILDKIT = '1'  // Enable BuildKit to avoid legacy builder warning
    }
    agent {
        label 'K-M'
    }
    stages {
        stage('Git') {
            steps {
                git url: 'https://github.com/YaswanthKumarDesineedi/Website-PRT-ORG.git', branch: 'main'
            }
        }
        stage('Docker') {
            steps {
                sh 'docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                sh 'docker build . -t yaswanth21/prt-task'
                sh 'docker push yaswanth21/prt-task'
            }
        }
        stage('K8s') {
            steps {
                sh 'kubectl apply -f deploy.yml'
                sh 'kubectl apply -f service.yml'
            }
        }
    }
}

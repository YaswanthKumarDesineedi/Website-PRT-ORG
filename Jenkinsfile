pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dhubcred')
    }
    agent {
        label 'K-M'
    }
    stages {
        stage('Git') {
            steps {
                git url: 'https://github.com/YaswanthKumarDesineedi/Website-PRT-ORG', branch: 'main'
            }
        }
        stage('Docker') {
            steps {
                sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                sh 'sudo docker build /home/ubuntu/jenkins/workspace/Test-Prt -t yaswanth21/prt-task'
                sh 'sudo docker push yaswanth21/prt-task'
            }
        }
        stage('K8s') {
            steps {
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}

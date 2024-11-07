pipeline {
    agent any
    stages {
        stage('git scm update') {
            steps {
                git url: 'https://github.com/KangDaeYoung/project1.git', branch: 'main'
            }
        }
        stage('delivery and deployment') {
            steps {
                sh '''
                ansible master -m copy -a "src=testpod2.yml dest=/root/testpod2.yml" --become 
                sudo docker build -t 211.183.3.199/testpj/jenkins:1.0 .
                sudo docker push 211.183.3.199/testpj/jenkins:1.0
                ansible master -m shell -a "docker image pull 211.183.3.199/testpj/jenkins:1.0" --become
                ansible master -m shell -a "kubectl apply -f /root/testpod2.yml" --become
                '''
            }
        }
    }
}

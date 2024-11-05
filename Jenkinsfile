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
                ansible master -m copy -a "src=testpod.yml dest=/root/testpod.yml" --become
                sudo docker build -t kangdaeyoung/project1:test .
                sudo docker push kangdaeyoung/project1:test
                ansible master -m shell -a "kubectl apply -f testpod.yml" --become
                '''
            }
        }
    }
}

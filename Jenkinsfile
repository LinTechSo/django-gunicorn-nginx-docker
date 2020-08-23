pipeline {
    agent none
    stages {
        stage('Build'){
            agent {
                label 'parham'
            }
            steps {
                sh 'docker-compose up -d --build'

                sh 'docker tag ppython_app localhost:443/ppython_app:new_v1'
                sh 'docker push localhost:443/ppython_app:new_v1'

                sh 'docker tag nginx localhost:443/nginx:1.17'
                sh 'docker push localhost:443/nginx:1.17'
            }
        }
        stage('Prod'){
            agent{
                label 'master'
            }
            steps {
                sh 'docker pull 192.168.1.4:443/ppython_app:new_v1'
                sh 'docker pull 192.168.1.4:443/nginx:1.17'
                sh 'docker run -d nginx:1.17'
                sh 'docker run -d ppython_app:new_v1'
            }
        }
    }
}

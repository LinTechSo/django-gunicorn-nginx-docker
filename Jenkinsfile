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
                sh 'docker rm -f django-gunicorn'

                sh 'docker tag nginx localhost:443/nginx:1.17'
                sh 'docker push localhost:443/'
                sh 'docker rm -f ngx'
            }
        }
        stage('Prod'){
            agent{
                label 'master'
            }
            steps {
                sh 'docker pull localhost:443/ppython_app:new_v1'
                sh 'docker pull localhost:443/nginx:1.17'
                sh 'docker run -d --name ngx nginx:1.17'
                sh 'docker run -d --name django ppython_app:new_v1'
            }
        }
    }
}

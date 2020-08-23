pipeline {
    agent none
    stages {
        stage('Build'){
            agent {
                agent { label 'parham'}
            }
            steps {
                'sh docker-compose up --build'

                'sh docker tag django-gunicorn localhost:443/django:new_v1'
                'sh docker push localhost:443/django:new_v1'

                'sh docker tag ngx localhost:443/ngx:new_v1'
                'sh docker push localhost:443/ngx:new_v1'
            }
        }
        stage('Prod'){
            agent{
                agent {label 'master'}
            }
            steps {
                'sh docker pull 192.168.1.4:443/django:new_v1'
                'sh docker pull 192.168.1.4:443/ngx:new_v1'
                'sh docker run -d ngx:new_v1'
                'sh docker run -d django:new_v1'
            }
        }
    }
}

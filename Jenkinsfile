pipeline {
    agent none
    stages {
        stage('Build'){
            agent {
                label 'parham'
            }
            steps {
                sh './Deploy/deploy.sh'
                sh 'cd Deploy/ && docker-compose up -d --build'
                sh './Deploy/test.sh'
                sh 'docker rm -f django-gunicorn'
                sh 'docker rm -f ngx'
            }
        }
        stage('Deploy'){
            agent{
                label 'parham'
            }
            steps {
                echo '> Deploying the application ...'
                ansiblePlaybook credentialsId: 'ansible',inventory: 'hosts', playbook: 'site.yml'
            }
        }
   }
}

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker-compose build'
            }           
        }
        stage('Test') {
            steps {
                sh 'docker-compose run app npm test'
            }           
        }
        stage('Deploy') {
            steps {
                script {
                    def is_deploy = input(message: 'Deploy?', parameters: [choice(choices: ['Yes', 'No'])])
                    if (is_deploy == 'Yes') {
                        sh 'docker-compose up -d'
                    }
                }
            }          
        }        
    }
    post {
        failure {
            sh 'docker-compose down'
        }
    }
}
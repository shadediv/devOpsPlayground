pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                cd simple_webserver
                aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 352708296901.dkr.ecr.eu-west-2.amazonaws.com
                docker build ecr-shadyash
                docker tag ecr-shadyash:latest 352708296901.dkr.ecr.eu-west-2.amazonaws.com/ecr-shadyash:latest
                docker push 352708296901.dkr.ecr.eu-west-2.amazonaws.com/ecr-shadyash:latest
                '''
            }
        }
        stage('Test the tests') {
            steps {
                echo 'Testing..'
                sh "cd youtubeBot"
            }
        }
        stage('Deploy the deployment') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
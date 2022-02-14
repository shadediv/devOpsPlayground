pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                echo "step 1 completed"
                echo "step 2 completed"
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
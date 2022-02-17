pipeline {

    environment{
        DockerUrl="352708296901.dkr.ecr.eu-west-2.amazonaws.com"
        Image="ecr-shadyash"
    }

    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                tag="${BRANCH_NAME}_${BUILD_NUMBER}"
                #cd simple_webserver
                #aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin ${DockerUrl}
                #docker build -t ${Image}:${tag} .
                #docker tag ${Image}:${tag} ${DockerUrl}/${Image}:${tag}
                #docker push ${DockerUrl}/${Image}:${tag}
                '''
            }
        }
        stage('Test the tests') {
            when{env.CHANGE_ID}
                steps {
                    echo 'Testing..'
                    sh "cd youtubeBot"
                }
            else
                steps {
                    echo 'Testing..'
                    sh "echo well its not a pull request"
                    sh "exit 1"
                }

        }
        stage('Deploy the deployment') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
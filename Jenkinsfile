pipeline {

    environment{
        DockerUrl="352708296901.dkr.ecr.eu-west-2.amazonaws.com"
        Image="ecr-shadyash"
    }

    agent any
    stages {
        stage('Build') {
            when { anyOf { branch "master"; branch "dev" }}
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
            when{ changeRequest() }
            steps {
                echo 'Testing..'
                sh 'python -m unittest simple_webserver/tests/test_flask_web.py'
            }
        }
        stage('Deploy the deployment') {
            steps {
                echo 'Deploying....'
            }
        }
         stage('Deploy - dev') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Deploy - prod') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Provision') {
            when { changeset "infra/**" }
            input {
                message "Do you want to proceed for infrastructure provisioning?"
            }
            steps {
                // copyArtifacts filter: 'infra/dev/terraform.tfstate', projectName: '${JOB_NAME}'
                echo 'Provisioning....'
                // archiveArtifacts artifacts: 'infra/dev/terraform.tfstate', onlyIfSuccessful: true
            }
        }
    }
}
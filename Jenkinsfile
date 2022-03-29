pipeline {

    environment{
        DockerUrl="352708296901.dkr.ecr.eu-west-2.amazonaws.com"
        Image="ecr-shadyash"
    }

    //agent { label "ec2-fleet" }

    agent any

    stages {
        stage('Build') {
            when { anyOf { branch "master"; branch "dev" }}
            steps {
                echo 'Building..'
                echo 'its in temp-for-jenkins'
            }
        }
        stage('Test the tests') {
            when{ changeRequest() }
            steps {
                echo 'Testing..'
                sh '''
                #pip3 install -r simple_webserver/requirements.txt
                #python3 -m unittest simple_webserver/tests/test_flask_web.py
                '''
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
            when { allOf { branch "dev"; changeset "infra/**" } }
            steps {
                sh "cd infra"
                sh "cd dev"
                sh "terraform init"
                sh "terraform plan"
                // copyArtifacts filter: 'infra/dev/terraform.tfstate', projectName: '${JOB_NAME}'
                // archiveArtifacts artifacts: 'infra/dev/terraform.tfstate', onlyIfSuccessful: true
            }
        }
    }
}
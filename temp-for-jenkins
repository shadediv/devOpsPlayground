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
                sh '''


                #**** build docker image ****
                #ec2-metadata
                #tag="${BRANCH_NAME}_${BUILD_NUMBER}"
                #cd simple_webserver
                #aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin ${DockerUrl}
                #docker build -t ${Image}:${tag} .
                #docker tag ${Image}:${tag} ${DockerUrl}/${Image}:${tag}
                #docker push ${DockerUrl}/${Image}:${tag}


                #**** build python package artifact ****
                #cd package_demo
                #pip3 install wheel
                #python3 setup.py sdist bdist_wheel
                #pip3 install twine
                #aws codeartifact login --tool twine --repository CodeArtifactRepo-shadyash --domain artifactory-shadyash --domain-owner 352708296901 --region eu-west-2
                #python3 -m twine upload dist/* --repository codeartifact
                '''
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
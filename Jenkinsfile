pipeline {
    agent any
    parameters {
        booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Select to deploy the function')
        booleanParam(name: 'UN-DEPLOY', defaultValue: true, description: 'Select to un-deploy the function)
    }

    stages {
        stage('Build') {
            steps {
                script{
                    sh 'npm install'
                    sh 'zip -r function.zip'
                }
            }
        }
        stage('Deploy Lambda') {
            when {
                expression { params.DEPLOY }
            }
            steps {
                sh 'aws lambda create-function --function-name node-function --zip-file fileb://function.zip --handler handler --runtime nodejs14.x'
            }
        }
        
        stage('Undeploy Lambda') {
            when {
                expression { !params.DEPLOY }
            }
            steps {
                sh 'aws lambda delete-function --function-name node-function'
            }
        }
    }
}

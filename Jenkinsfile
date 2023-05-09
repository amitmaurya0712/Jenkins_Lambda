pipeline {
    agent any
    parameters {
        booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Select to deploy the function')
        booleanParam(name: 'UN-DEPLOY', defaultValue: true, description: 'Select to un-deploy the function')
    }

    stages {
        stage('Clone the Repo') {
            steps{
                git branch: 'main', url: 'https://github.com/amitmaurya0712/Jenkins_Lambda.git'
            }
        }

        stage('Build') {
            steps {
                script{
                    sh 'npm install'
                    sh 'zip -r function.zip index.js package.json'
                }
            }
        }
        stage('Deploy Lambda') {
            when {
                expression { params.DEPLOY }
            }
            steps {
                // step([$class: 'LambdaCreateFunctionBuilder', credentialsId: 'aws-credentials', region: 'us-west-2', functionName: 'node-function', runtime: 'python3.9', artifact: 'function.zip', handler: 'handler', role: 'arn:aws:iam::964715276857:role/aws-lambda'])
                 deployLambda([alias: '', artifactLocation: 'function.zip', awsAccessKeyId: 'AKIA6BHMC5I434G2LJ6P', awsRegion: 'us-west-2', awsSecretKey: '{AQAAABAAAAAwIcemqGdRWlC6PazxEjzqELWRivZSdxNv90m3Z7P7OTEtMk3n1pW68LPasVSgn8hY5dju0kXyCql0lIo1nsnxDg==}', deadLetterQueueArn: '', description: '', environmentConfiguration: [kmsArn: ''], functionName: 'node-function', handler: 'handler', memorySize: '', role: 'arn:aws:iam::964715276857:role/aws-lambda', runtime: 'nodejs14.x', securityGroups: '', subnets: '', timeout: '', updateMode: 'full'])
        }
        }
        
        stage('Undeploy Lambda') {
            when {
                expression { !params.UN-DEPLOY }
            }
            steps {
                sh 'aws lambda delete-function --function-name node-function'
            }
        }
    }
}


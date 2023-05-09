pipeline {
    agent any
    parameters {
        booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Select to deploy the function')
        booleanParam(name: 'UNDEPLOY', defaultValue: true, description: 'Select to un-deploy the function')
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
                sls deploy 
        }
        }
        // stage('Undeploy Lambda') {
        //     when {
        //         expression { params.UNDEPLOY }
        //     }
        //     steps {
        //         sls remove
        //     }
        // }
    }
}


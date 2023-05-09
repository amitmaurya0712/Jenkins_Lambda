pipeline {
  agent any
  environment {
    AWS_ACCESS_KEY_ID = credentials('aws-credentials-id').AWS_ACCESS_KEY_ID
    AWS_SECRET_ACCESS_KEY = credentials('aws-credentials-id').AWS_SECRET_ACCESS_KEY
  }
  stages {
    stage('Build') {
      steps {
        // Build your Node.js function and create a function.zip file
        sh 'npm install'
        sh 'npm run build'
        sh 'zip -r function.zip .'
      }
    }
    stage('Deploy') {
      steps {
        // Deploy the AWS Lambda function
        sh 'aws lambda create-function --function-name myff-function --runtime nodejs14.x --role arn:aws:iam::964715276857:role/aws-lambda --handler handler --zip-file fileb://function.zip --region us-west-2'
      }
    }
  }
}

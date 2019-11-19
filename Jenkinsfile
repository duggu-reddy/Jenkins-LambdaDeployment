def bucket = 'duggu-9988'
def functionName = 'APIintegration-Lambda'
def region = 'eu-east-1'

node{
    stage('Checkout'){
        checkout scm
    }

    stage('Build'){
        sh "id"
        sh "zip deployment-lambda.zip *"
    }

    stage('Push'){
        sh "/var/lib/jenkins/.local/bin/aws s3 cp deployment-lambda.zip s3://${bucket}"
    }

    stage('Deploy'){
        sh "/var/lib/jenkins/.local/bin/aws lambda update-function-code --function-name ${functionName} \
                --s3-bucket ${bucket} \
                --s3-key deployment-lambda.zip \
                --region ${region}"
    }
}


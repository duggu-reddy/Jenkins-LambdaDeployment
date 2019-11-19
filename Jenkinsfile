def bucket = 'duggu-9988'
def functionName = 'APIintegration-Lambda'
def region = 'eu-east-1'

node('slaves'){
    stage('Checkout'){
        checkout scm
    }

    stage('Build'){
        sh "zip ${commitID()}.zip *"
    }

    stage('Push'){
        sh "aws s3 cp ${commitID()}.zip s3://${bucket}"
    }

    stage('Deploy'){
        sh "aws lambda update-function-code --function-name ${functionName} \
                --s3-bucket ${bucket} \
                --s3-key ${commitID()}.zip \
                --region ${region}"
    }
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}

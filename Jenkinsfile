pipeline {
    agent {
        label 'Agent-1'
    }
    environment{
       APP_VERSION = ''
       AWS_REGION='us-east-1'
    }
     options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
    }    
    stages {
       stage('Read Package Version') {
            steps {
                script {
                    // Read the entire package.json file into a Groovy map/object
                    def packageJSON = readJSON file: 'package.json'

                    // Access the version property and set it as an environment variable
                    APP_VERSION = packageJSON.version

                    // Print the version to the console output
                    echo "Project version: ${APP_VERSION}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script{
                    sh '''
                    npm install
                    '''
                }
            }
        }
        stage('Docker Build') {            
            steps {               
                    withAWS(credentials: 'aws-auth', region: "${AWS_REGION}") {
                    script{
                    sh """
                        aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin 583084550155.dkr.ecr.us-east-1.amazonaws.com
                        docker build -t 583084550155.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${APP_VERSION}
                        docker push 583084550155.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${APP_VERSION}
                    """
                }
            }
        }
    }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        success { 
            echo 'Hello Success!'
        }
        failure { 
            echo 'Hello, Failure!'        
    }
}
}
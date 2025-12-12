pipeline {
    agent {
        label 'Agent-1'
    }
    environment{
       APP_VERSION = ''
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
                    env.APP_VERSION = packageJSON.version

                    // Print the version to the console output
                    echo "Project version: ${env.APP_VERSION}"
                }
            }
        }
        stage('Build') {
            steps {
                script{
                    sh '''
                    echo "Hello Build"
                    '''
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {            
            steps {
                echo 'Deploying....'
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
        changed { 
            echo 'Hello!.. Changed!'
        }
    }
}

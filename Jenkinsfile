pipeline {
    agent {
        label 'Agent-1'
    }
    // environment{
    //     course="jenkins"
    // }
     options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
    }    
    stages {
        stage('Build') {
            steps {
                script{
                sh """
                echo "Hello Build"
                """
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
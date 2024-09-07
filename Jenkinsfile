pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm') //plugin for colors
    }
    stages {
        stage('init') {
            steps {
                sh '''
                ls -ltr
                '''
            }
        }
        
    }
    post {  //executes based on whether if it is success or failure
        always { 
            echo 'I will always say Hello again!'
            deleteDir() //this will delete the directory created for every build which is recommended.
        }
        success { 
            echo 'I will run when pipeline is success'
        }
        failure { 
            echo 'I will run when pipeline is failure'
        }
    }
}

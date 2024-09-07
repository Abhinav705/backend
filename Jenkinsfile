pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm') //plugin for colors
    }
    environment{
        def appVersion = '' //variable declaration
    }
    stages {
        stage('Read the version'){
            steps{
                script{ //we need to take the version from the package.json file.. we need this version for zipping process
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "Application Version: $appVersion"
                }
            }
        }
        stage('Install Dependencies') {
            steps { //npm install is to download the dependencies in the agent
                sh '''
                npm install 
                ls -ltr
                echo "Application Version: $appVersion"
                '''
            }
        }
        // stage('Build'){
        //     steps{
        //         sh '''
        //         zip -q -r backend-${appVersion}.zip * -x Jenkinsfile -x backend-${appVersion}.zip
        //         ls -ltr
        //         '''
        //     }
        // }
        
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

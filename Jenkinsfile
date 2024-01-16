pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven'
    }

    stages {
        stage('Build') {
            steps {
                bat "\"${MAVEN_HOME}\\bin\\mvn\" clean package"
            }
        }

        stage('Stop Service') {
            steps {
             	     bat "net stop HRMS"
             	     sleep time: 10, unit: 'SECONDS'
             	     bat 'sc query HRMS | find "STATE" | find "STOPPED" && echo "Service stopped"'  
            }
        }

 		stage('Copy Jar File') {
            steps {
                bat "copy /Y target\\HRMS.jar G:\\HRMS_API\\HRMS"
            }
        }
    }
    post {
        always {
           bat "nssm start HRMS"
        }
    }
}
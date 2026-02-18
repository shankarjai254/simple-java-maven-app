pipeline {
    agent any
    tools {
        maven 'Maven_3.8.8_System'   // name configured in Global Tool Configuration
        jdk 'javajenkins'        // adjust to your setup
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') { 
            steps {
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
    }
}

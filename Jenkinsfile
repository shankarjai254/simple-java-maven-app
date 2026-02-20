pipeline {
    agent any
    tools {
        maven 'Maven_3.8.8_System'   // name configured in Global Tool Configuration
        jdk 'javajenkins'        // adjust to your setup f3feqfeqf effefe
    }
    stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Java_project \
                    -Dsonar.projectKey=Java_project '''
                }
            }
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

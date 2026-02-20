pipeline {
    agent any

    tools {
        maven 'Maven_3.8.8_System'
        jdk 'javajenkins'
    }
     environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }

    stages {
        stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Java_project \
                    -Dsonar.projectKey=Java_project '''
                }
            }
        }

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

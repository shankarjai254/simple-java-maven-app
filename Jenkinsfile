pipeline {
    agent any

    tools {
        maven 'Maven_3.8.8_System'
        jdk 'javajenkins'
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

        stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=Java_project \
                    -Dsonar.projectName=Java_project
                    '''
                }
            }
        }
    }
}
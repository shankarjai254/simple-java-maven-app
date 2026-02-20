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
                    sh ''' $SCANNER_HOME/bin/sonar-scanner clean verify sonar:sonar -Dsonar.projectKey=Java_project -Dsonar.projectName='Java_project'  -Dsonar.token=sqp_2259f85580e3a34e236abaf216aec74cb895a626 '''
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

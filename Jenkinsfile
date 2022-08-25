pipeline {
    // agent {
    //     docker {
    //         image 'maven:3-alpine'
    //         args '-v /root/.m2:/root/.m2'
    //     }
    // }
    agent any
    tools {
        maven 'apache-maven-3.0.1'
        // sonarqube
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

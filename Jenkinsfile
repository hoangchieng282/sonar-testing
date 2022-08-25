pipeline {
    // agent {
    //     docker {
    //         image 'maven:3-alpine'
    //         args '-v /root/.m2:/root/.m2'
    //     }
    // }
    agent any
    tools {
        maven 'MAVEN-PATH'
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
        stage('Sonarqube') {
            steps {
                sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=jenkins-test \
                    -Dsonar.host.url=http://sonarqube:9000 \
                    -Dsonar.login=723f4a3c180ec5e569fabfb364a41053b7771f63
                '''
            }
        }
    }
}

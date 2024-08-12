pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'  // Maven Docker image with JDK 11
            args '-v /root/.m2:/root/.m2'  // Mounts the Maven repository cache
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package'  // Build the project without running tests
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'  // Run the tests
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'  // Archive the test results
                }
            }
        }
    }
}

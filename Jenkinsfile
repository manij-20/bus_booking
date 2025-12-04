pipeline {
    agent { label 'java' }

    tools {
        jdk 'JDK17'
        maven 'maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'feature-1', url: 'https://github.com/manij-20/bus_booking.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=false'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Run Application') {
            steps {
                sh 'mvn spring-boot:run'
                dir('/var/lib/jenkins/workspace/Bus_booking_feature-1/target') {
                    sh '''
                        # nohup java -jar bus-booking-app-1.0-SNAPSHOT.jar > app.log 2>&1 &
                        # echo "Application started"
                    '''
                }
            }
        }
    }
}

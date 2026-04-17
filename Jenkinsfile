pipeline {
    agent any  // Use any available agent

    tools {
        maven 'Maven'  // Ensure this matches the name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SuhasNazare/MyMavenWebApp01.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'  // Run unit tests
            }
        }

        
        
       
        stage('Run Application') {
            steps {
                // -Djetty.http.port=8082 tells Jetty to stay out of Jenkins' way
                sh 'sh 'mvn jetty:start -Djetty.http.port=8082 && sleep 10 && mvn jetty:stop -Djetty.stopPort=8083 -Djetty.stopKey=STOP''
            }
        }

        
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

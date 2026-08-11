pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-21'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    
    stages {
        stage('Initialize') {
            steps {
                echo "Running inside Docker container: maven:3.9.6-eclipse-temurin-21"
                sh 'java -version'
                sh 'mvn -version'
            }
        }
        stage('Build Environment Test') {
            steps {
                echo "Compiling and packaging..."
                sh 'mvn clean install'
            }
        }
    }
    
    post {
        always {
            echo "Pipeline execution completed. Container will now be destroyed."
        }
    }
}

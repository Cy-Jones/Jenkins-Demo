pipeline {
    agent {
        docker {
            // This pulls a container pre-loaded with Java 21 and Maven
            image 'maven:3.9.6-eclipse-temurin-21'
            // We mount the local Maven repository to cache dependencies between builds
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
                // Tying this back to your Practical 2 Maven project execution
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

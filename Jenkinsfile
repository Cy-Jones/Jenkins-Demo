pipeline {
    agent any // Run on the Mac host first to establish the environment
    
    environment {
        // Forces Jenkins to look in Homebrew and Docker installation paths on macOS
        PATH = "/usr/local/bin:/opt/homebrew/bin:${env.PATH}" 
    }

    stages {
        stage('Build with Maven Container') {
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
        }
    }
    
    post {
        always {
            echo "Pipeline execution completed. Container will now be destroyed."
        }
    }
}

pipeline {
    agent any // Runs natively on your Mac where Docker works
    
    stages {
        stage('Build inside Docker') {
            steps {
                // Manually run the Maven build inside the exact same container image
                sh '''
                    docker run --rm \
                    -v "$HOME/.m2:/root/.m2" \
                    -v "$WORKSPACE:$WORKSPACE" \
                    -w "$WORKSPACE" \
                    maven:3.9.6-eclipse-temurin-21 \
                    mvn clean install
                '''
            }
        }
    }
    
    post {
        always {
            echo "Pipeline execution completed."
        }
    }
}

pipeline {
    agent any // Run natively on the Mac host where docker is verified

    stages {
        stage('Run Maven Build via Docker Container') {
            steps {
                echo "Bypassing buggy Jenkins agent plugins. Running Docker manually via shell..."
                
                // Explicitly run the build step inside a standalone container block
                sh '''
                    /usr/local/bin/docker run --rm \
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

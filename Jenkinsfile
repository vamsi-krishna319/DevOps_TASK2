pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-node-app"
        CONTAINER_NAME = "my-node-container"
        PORT = "3000"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Pulling latest code from GitHub..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing Node.js dependencies..."
                sh '''
                    if [ -f package.json ]; then
                        npm install
                    else
                        echo "package.json not found!"
                        exit 1
                    fi
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running test cases..."
                sh '''
                    if npm test ; then
                        echo "Tests passed"
                    else
                        echo "Tests failed"
                        exit 1
                    fi
                '''
            }
        }

        stage('Docker Build') {
            steps {
                echo "Building Docker image..."
                sh '''
                    docker build -t $IMAGE_NAME:latest .
                '''
            }
        }

        stage('Docker Deploy') {
            steps {
                echo "Deploying Docker container..."

                // Stop old container if exists
                sh '''
                    if [ "$(docker ps -aq -f name=$CONTAINER_NAME)" ]; then
                        echo "Stopping old container..."
                        docker stop $CONTAINER_NAME || true
                        echo "Removing old container..."
                        docker rm $CONTAINER_NAME || true
                    fi
                '''

                // Run new container
                sh '''
                    docker run -d \
                        --name $CONTAINER_NAME \
                        -p $PORT:$PORT \
                        $IMAGE_NAME:latest
                '''

                echo "Deployment completed successfully!"
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs."
        }
    }
}

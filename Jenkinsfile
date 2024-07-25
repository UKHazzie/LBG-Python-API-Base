pipeline {
    agent any
    environment {
        GCR_CREDENTIALS_ID = 'cf126c88-4640-4295-b888-08dcbbf88453' // The ID you provided in Jenkins credentials
        IMAGE_NAME = 'richards_week3_proj'
        GCR_URL = 'europe-west1-docker.pkg.dev/lbg-mea-20/gcr-richard-week3-project'
    }
    stages {
        stage('Build and Push to GCR') {
            steps {
                script {
                    // Authenticate with Google Cloud
                    withCredentials([file(credentialsId: GCR_CREDENTIALS_ID, variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                        sh 'gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS'
                    }
                // Configure Docker to use gcloud as a credential helper
                sh 'echo "configure docker"'
		sh 'gcloud auth configure-docker --quiet'
		
                // Build the Docker image
                sh 'echo "build docker";
		sh "docker build -t ${GCR_URL}/${IMAGE_NAME}:${BUILD_NUMBER} ."
                // Push the Docker image to GCR
                sh 'echo "Push docker"'
		sh "docker push ${GCR_URL}/${IMAGE_NAME}:${BUILD_NUMBER}"
                }
            }
        }
    }
}

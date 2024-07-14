pipeline {
    agent any


    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/PallawiDutta/helloworld.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
        
        stage('Docker Image Build/Publish') {
            steps {
                bat 'docker build -t helloworld .'
                bat 'docker login -u pallawidutta -p Dutta123@'
                bat 'docker tag helloworld pallawidutta/helloworld'
                bat 'docker push pallawidutta/helloworld'
            }
        }
            
        stage('Docker Container Creation') {
            steps {
                script {
                    def containerName = "helloworld"

                    echo "Creating new container ${containerName}..."
                    bat "docker pull pallawidutta/helloworld"
                    bat "docker run -itd --name ${containerName} -p 8081:8080 pallawidutta/helloworld"
                } 
            }  
        }
    }

    post {
        always {
            // Actions to perform after the pipeline, e.g., clean up
            echo 'Cleaning up...'
        }

        success {
            echo 'Pipeline succeeded!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}

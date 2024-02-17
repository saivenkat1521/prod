pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    docker.build('992382769101.dkr.ecr.ap-south-1.amazonaws.com/my-timeoff-app/my-timeoff-app:latest')
                }
            }
        }

        stage('Push to ECR') {
            steps {
                script {
                    // Push image to ECR
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIA6ODU7K7GWWF4WVSM', credentialsId: 'aws-creds-id', secretKeyVariable: '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']]) {
                        sh "aws ecr get-login-password --region ap-south-1 | docker login --venkatnaidu15@yahoo.com AWS --Sritha@21-stdin 992382769101.dkr.ecr.ap-south-1.amazonaws.com/my-timeoff-app/my-timeoff-app:latest"
                        docker.push '992382769101.dkr.ecr.ap-south-1.amazonaws.com/my-timeoff-app/my-timeoff-app:latest/my-timeoff-app:latest'
                    }
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                script {
                    // Deploy to EKS using kubectl
                    sh "kubectl apply -f k8s/deployment.yaml"
                }
            }
        }
    }
}

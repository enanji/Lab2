pipeline {
    agent { label 'java' }

    triggers {
    pollSCM('H/2 * * * *')
}

    stages {
        stage('Git Clone') {
            steps {
                echo "Cloning GitHub repo..."
                checkout scm
            }
        }

        stage('Run Kubernetes Manifests') {
            steps {
                echo "Applying Kubernetes YAML files..."
                sh '''
                  kubectl apply -f deployment.yaml
                  kubectl apply -f service.yaml
                  kubectl get deployment
                  kubectl get pods
                  kubectl get rs
                '''
            }
        }
        stage('verification') {
            steps {
                sh "curl 192.168.49.2:30303"
            }
        }
    }
}
pipeline {
    agent any
    environment {
		DOCKER_HUB_REPO = 'dataguru97/gitops-testing'
		DOCKER_HUB_CREDENTIALS_ID = 'gitops-dockerhub-token'
    }
    stages {
        stage('Checkout Github') {
            steps {
                echo 'Checking out code from GitHub...'
		        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/data-guru0/GitOPS-testing.git']])
            }
        }        
        stage('Build Docker Image') {
            steps {
                script {
					echo 'building docker image...'
					dockerImage = docker.build("${DOCKER_HUB_REPO}:latest")
				}
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                 script {
					echo 'pushing docker image to DockerHub...'
					docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_HUB_CREDENTIALS_ID}"){
						dockerImage.push('latest')
						}
					}
            }
        }
        stage('Install Kubectl & ArgoCD CLI') {
            steps {
                echo 'Installing Kubectl and ArgoCD CLI...'
            }
        }
        stage('Apply Kubernetes & Sync App with ArgoCD') {
            steps {
                echo 'Applying Kubernetes and syncing with ArgoCD...'
            }
        }
    }
}


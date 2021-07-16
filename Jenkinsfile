pipeline {
    environment {
        registry = "trainerdheerajsharma/demoapp"
        registryCredential = 'docker'
        dockerImage = ''
    }
    agent any
    
    tools {nodejs "node"}

    stages {
        
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/trainer-dheeraj/git-tutorial'
            }
        }
        stage('Install') {
            steps {
                bat 'npm install'
            }
        }
        stage('test') {
            steps {
                bat 'npm test'
            }
        }   
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Verify') {
            steps {
                echo 'The software is now deployed!'
            }
        }
    }    
}

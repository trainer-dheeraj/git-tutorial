pipeline {
    environment {
        registry = "trainerdheerajsharma/demoapp"
        registryCredential = 'docker'
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
                    docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }   
        stage('Deploy') {
            steps {
                echo 'The software will now be deployed!'
            }
        }
    }    
}

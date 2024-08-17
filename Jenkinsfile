pipeline {
    agent any

    tools {nodejs "nodejs"}

    stages {
        stage('node setup') { 
            steps {
                sh 'npm install --force' 
            }
        }
        stage('build'){
            steps{
                sh 'npm run build'
            }
        }
        stage('build'){
            steps{
                sh 'npm run build'
            }
        }
    }
}
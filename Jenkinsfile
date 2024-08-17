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
        stage("archive distro"){
            steps{
                // create zip
                //sh "zip -r distro-achieve.zip /distro"
                script{
                     zip zipFile: 'distro-achieve.zip', archive: false, dir: 'dist'
                }
            }
        }

        stage('Upload artifacts'){
            steps{
                uploadGithubReleaseAsset(
                    credentialId: 'GITHUB_TOKEN',
                    repository: 'immyemperor/cicd_angular',
                    tagName: 'v1.${env.BUILD_NUMBER}', 
                    uploadAssets: [
                            [filePath: 'distro-achieve.zip']
                    ]
                )
            }
        }
    }
}
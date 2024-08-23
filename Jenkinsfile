pipeline {
    agent any
    parameters {
        booleanParam(name: 'withAdminBuild', defaultValue: true, description: '')
    }

    environment {
        WITH_ADMIN_BUILD = $params.withAdminBuild
    }

    tools {nodejs "nodejs"}

    stages {
        stage('node setup') { 
            steps {
                sh 'npm install --force' 
            }
        }
        stage('build-with-admin'){
            when{
                expression {
                    return env.WITH_ADMIN_BUILD;
                }
            }
            steps{
                sh 'npm run build'
            }
        }
        stage('build-without-admin'){
            when{
                expression {
                    return !env.WITH_ADMIN_BUILD;
                }
            }
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
    post { 
         always { 
            cleanWs()
        }
    }
}
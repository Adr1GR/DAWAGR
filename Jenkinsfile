pipeline {
agent any

        stages {
            stage('SCM') {
                steps {
                    checkout([$class: 'GitSCM', branches: [[name: '*/developerAGR']],
                    extensions: [], userRemoteConfigs: [[url: 'https://github.com/Adr1GR/DAWAGR.git']]])
                }
            }
            stage('Test'){
                steps{
                    sh 'phpunit test'
                }
            }
            stage('Comprimir'){
                steps{
                    script{
                        zip archive: true, zipFile: 'last.zip'
                    }
                }
            }
            stage("Push"){
                steps{
                    sh 'git checkout master'
                    sh 'git merge developerAGR'
                    sh 'git push '
                }
            }
            stage("End"){
                steps{
                    archiveArtifacts artifacts: 'last.zip', followSymlinks: false
                    sh 'rm ./last.zip'
                }
            }
        }
    }
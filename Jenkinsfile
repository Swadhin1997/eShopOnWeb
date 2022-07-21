def project_folder = "/var/lib/jenkins/workspace/sample@2/src"

def JOB_NAME = 'DotnetSample'

def backup_folder = '/var/lib/jenkins/workspace/webbackup'

pipeline {



agent any

     options {

        timestamps()

    }



    stages {

       

        stage ("Clone Repository") {

                steps {

                   git branch: 'main', url: 'https://github.com/Swadhin1997/eShopOnWeb.git'

                }

            }  



        stage('Prep') {

            steps {

                script {

                    GIT_BRANCH=sh(returnStdout: true, script: 'git symbolic-ref --short HEAD').trim()

                    currentBuild.setDisplayName("#${currentBuild.number} [" + GIT_BRANCH + "]")

                    sh "export GIT_BRANCH=$GIT_BRANCH"

                }

            }

        }  

   

        stage ('Building dll') {

            steps {

               sh "dotnet build eShopOnWeb.sln"

            }  

        }  

        stage ('create backup') {
            steps {
                script {
                    echo "Copying project as backup"
                    sh "mkdir ${backup_folder}/${JOB_NAME}_${currentBuild.number}"
                    sh "cp -r ${project_folder} ${backup_folder}/${JOB_NAME}_${currentBuild.number}"
                }
            }
        }

            }
}


         

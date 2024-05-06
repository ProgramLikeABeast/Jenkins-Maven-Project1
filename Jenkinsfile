pipeline {
    agent any
    tools{
        maven 'local maven'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post{
                success{
                    echo 'begin archiving'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }  
        stage('deploy to staging'){
            steps{
                build job:'deploy-to-stage'
            }
        }
        stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'deploy to production?'
                }

                build job: 'deploy-to-production'
            }
            post {
                success {
                    echo 'successfully deployed to production.'
                }

                failure {
                    echo 'failed to deploy to production.'
                }
            }
        }

    }
}

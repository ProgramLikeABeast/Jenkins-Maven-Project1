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
    }
}

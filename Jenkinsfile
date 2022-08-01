pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

     stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.11.war', type: 'war']], credentialsId: 'e9cdd510-3c19-4625-921e-361132bb8ef3', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.178:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'DevOpsLab-SNAPSHOT', version: '0.0.11'
            }
        }
        
        // Stage3 : Deploying
        stage('Deploy'){
            steps{
                echo 'deploying...'
            }
        }


     }
     
}
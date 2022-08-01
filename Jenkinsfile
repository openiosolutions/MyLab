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
               nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.3-SNAPSHOT.war', type: 'war']], credentialsId: '86aad2cd-e279-4ba9-a4ce-f00ce430dc6a', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.178:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'RepoLab-SNAPSHOT', version: '0.0.3-SNAPSHOT'
            }
        }
        
        // Stage4 : Deploying
        stage('Deploy'){
            steps{
                echo 'deploying...'
            }
        }


     }
     
}
pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
     environment{
         ArtifactId = readMavenPom().getArtifactId()
          Version = readMavenPom().getVersion()
          Name = readMavenPom().getName()
          GroupId = readMavenPom().getGroupId()
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

         // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }
        
        // Stage5 : Deploying
        stage('Deploy'){
            steps{
                echo 'deploying...'
            }
        }


     }
     
}
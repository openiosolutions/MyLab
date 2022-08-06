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
                script{

                     def NexusRepo = Version.endsWith("SNAPSHOT") ? "RepoLab-SNAPSHOT" : "RepoLab-RELEASE"

               nexusArtifactUploader artifacts: 
               [[artifactId: "${ArtifactId}",
                classifier: '',
                 file: "target/${ArtifactId}-${Version}.war",
                  type: 'war']],
                   credentialsId: '86aad2cd-e279-4ba9-a4ce-f00ce430dc6a', 
                   groupId: "${GroupId}", nexusUrl: '172.20.10.178:8081',
                    nexusVersion: 'nexus3',
                     protocol: 'http',
                      repository: "${NexusRepo}",
                       version: "${Version}"
                }
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
        
        // Stage 5 : Deploying the build artifact to Apache Tomcat
        stage ('Deploy to Tomcat'){
            steps {
                echo "Deploying ...."
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'AnsibleController', 
                    transfers: [
                        sshTransfer(
                                cleanRemote:false,
                                execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy.yaml -i /opt/playbooks/hosts',
                                execTimeout: 120000
                        )
                    ], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)
                    ])
            
            }
        }

     }
     
}
@Library("Jenkins_shared") _


pipeline{
    
    agent any
    
    //options{
    //    timestamp()
    //}
    
    environment{
        MYENVVAR = "testenvvar"
    }
    
    parameters{
        string(name: "Name", defaultValue: "Fin", description: "my name is fin")
    }
    
    stages{
        stage("Build"){
            steps{
                echo "Build"
                helloVariable("Fin")
                echo "${MYENVVAR}"
                echo "${params.Name}"
                script{
                    utils.replaceString()
                }
            }
        }
        
        stage("Docker Build"){
            agent{
                docker{
                    image "node.latest"
                    args "-v ${WORKSPACE}/docker:/home/node"
                }
            }
            steps {
                sh """
                    node --version >/home/node/docker_node_version
                    npm
                """
            }
        }
        
        
        
      stage("Test"){
           steps {
               sh """
               cat index.html | grep "Deployed by Jenkins job: ${BUILD_NUMBER}"
               """
            }
        }
        
      stage("testing branches"){
          parallel{
            stage("Test on linux"){
                steps{
                    echo "Linux"
                }
            }
            stage("Test on windows"){
                steps{
                    echo "Windows"
               }
            }
          }
       } 
        stage("Deploy"){
            steps{
               echo "Deploy"             
            sshPublisher(publishers: [sshPublisherDesc(configName: 'Http', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'mv index.html /var/www/html/index.html', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'index.html')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])   
            }
        }
    }
    post {
        always{
            archiveArtifacts artifacts: 'index.html', followSymlinks: false
        }
        
        //cleanup{
        //    cleanWs()
        //}
    }
}


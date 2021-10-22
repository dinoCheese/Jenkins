@Library("Jenkins_shared") _


pipeline{
    
    agent any
    stages{
        stage("Build"){
            steps{
                build '1_freestyle'
                echo "Build"
                helloVariable("Fin")
                script{
                    utils.replaceString()
                }
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
            }
        }
        stage("other pipeline"){
            steps{
            sshPublisher(publishers: [sshPublisherDesc(configName: 'Http', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'mv webpage/index.html /var/www/html/index.html', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'build.tgz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}

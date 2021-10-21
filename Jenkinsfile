
def printFromFunction(){
  println("I am printing from a function")
}

pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "Build"
                printFromFunction()
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
    }
}













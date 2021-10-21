@Library("Jenkins_shared") _


def printFromFunction(){
  println("I am printing from a function")
}

def replaceString(){
  def text = readFile file: "index.html"
  text = text.replaceAll("%BUILD_NUMBER%", "${BUILD_NUMBER}")
  writeFile file: "index.html", text:text
}

pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "Build"
                helloVariable("Fin")
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













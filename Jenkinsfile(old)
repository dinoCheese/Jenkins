pipeline{

  agent any
  
  options {
    timestamp()
  }
  
  stages {
    stage("My first stage"){
      steps{
      echo "This is a step in my first stage"
      }
    }

    stage("2nd") {
      steps{
        sh 'printenv'
      }
    }
  }
}

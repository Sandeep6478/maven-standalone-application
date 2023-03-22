pipeline {
  agent any
  stages{
    stage('Fetch'){
      steps{
        git branch:'paac',url:'https://github.com/Sandeep6478/maven-standalone-application.git'
      }
    }
    stage('Build'){
      steps{
        sh'mvn install'
      }
    }
    stage('Test'){
      steps{
        sh 'mvn test'
      }
    }
  }
}

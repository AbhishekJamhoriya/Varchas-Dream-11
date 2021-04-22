pipeline {
  agent any
  
  stages {
    stage("git-Checking "){
        steps{
            echo "Checking out from git Repo";
            git 'https://github.com/AbhishekJamhoriya/Varchas-Dream-11.git'
        }
    }
    stage('Compile') {
      steps {
        echo "Compiling App and its dependencies"
        
        bat script:'./gradlew compileDebugSources'
      }}
    
    stage('Unit tests') {
      steps {
        echo "Running Unit Tests"
        
        bat './gradlew testDebugUnitTest'
        
       

      }}
     
    stage('Build APK') {
      steps {
        echo "Building APK"
        bat './gradlew assembleDebug'   
      }
    }
      
    
     
    stage('Deploy') {
      
      steps {
        echo "Deploying APK"
        
        bat './gradlew assembleRelease'
      }
    }
    
  post{
    always{
        echo "This will run always";
        
    }
    success{
        echo "This will run only if successful";
    }
    failure{
        echo "This will only run if system failed";
    }
    unstable{
        echo "This will run only if the run was marked as unstable";
    }
    changed{
        echo "This will run only if the state of the piipline was changed"
    }
}
}
}

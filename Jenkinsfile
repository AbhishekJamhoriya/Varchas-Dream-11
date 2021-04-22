pipeline {
  agent {
    // Run on a build agent where we have the Android SDK installed
    label 'android'
  }
  options {
    // Stop the build early in case of compile or test failures
    skipStagesAfterUnstable()
  }
  stages {
    stage('Permissions') {
      // This stage is set to access some permissions in Ubuntu machine
      steps {
        
         echo "-------------------Asking for permissions--------------------"
        
        bat 'ls -la ./gradlew'
        bat 'chmod +x ./gradlew'
        bat 'ls -la ./gradlew'
      }
      post {
        success {
          // Notify permissions granted
           echo "Permissions granted!!"
        }
        failure {
          // Notify permissions denied
          echo "Oops!! Permissions denied.'"
        }
      }
    }
    stage('Compile') {
      steps {
        echo "-------------------Compiling App and its dependencies--------------------'"
        
        // Compile the app and its dependencies
        bat './gradlew compileDebugSources'
      }
      post {
        success {
          // Notify compile successful
           echo "'App compiled successfully.'"
        }
        failure {
          // Notify compile failed
          echo "Compile failed!!'"
        }
      }
    }
    stage('Unit tests') {
      steps {
        echo "'-------------------Running Unit Tests--------------------'"
        
        // Compile and run the unit tests for the app and its dependencies
        bat './gradlew testDebugUnitTest'
        
       

      }
      post {
        success {
          // Notify tests successful
          echo "'All tests passed successfully.'"
        }
        failure {
          // Notify tests failed
          echo "'Some tests are failing.'"
        }
      }
    }
    stage('Build APK') {
      steps {
        echo "'-------------------Building APK--------------------'"
        
        // Finish building and packaging the APK
        bat './gradlew assembleDebug'

        
      }
      post {
        success {
          // Notify build successful
          echo "'APK build successful'"
        }
        failure {
          // Notify build failed
          echo "'APK build failed.'"
        }
      }
    }
    stage('Lint Check') {
      steps {
        sh "echo '-------------------Running Lint checks--------------------'"
        
        // Run Lint and analyse the results
        bat './gradlew lintDebug'
        
      }
      post {
        success {
          // Notify lint checks successful
          echo "'Lint checks successful.'"
        }
        failure {
          // Notify lint checks failed
           echo "'Lint checks failed.'"
        }
      }
    }
    stage('Deploy') {
      
      steps {
        echo "'-------------------Deploying APK--------------------'"
        
        // Build the app in release mode
        bat './gradlew assembleRelease'

        // Archive the APKs so that they can be downloaded from Jenkins
        
        
      }
      post {
        success {
          // Notify build succeeded
          echo "'Congrqatulations! Build successful.'"
        }
      }
    }
  }
  post {
    failure {
      // Notify build failed
      echo "'Oops! Build ${env.BUILD_NUMBER} failed; ${env.BUILD_URL}'"
    }
  }
}

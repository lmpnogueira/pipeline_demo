pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh "chmod u+x build_script.sh"
        sh "./build_script.sh"
      }
    }
    stage('Test') {
     parallel {
       stage('Test On Windows') {
         steps {
           echo "Running tests on Windows"
         }
       }
       stage('Test On Linux') {
         steps {
           echo "Running tests on Linux"
         }
       }
     }
   }
   stage('Confirm Deploy to staging') {
     steps {
       timeout(time: 60, unit: 'SECONDS') {
         input(message: 'Okay to Deploy?', ok: 'Let\'s Do it!')
       }
     }
   }
   stage('Deploy to Staging') {
     steps {
       echo "Deploying to staging..."
     }
   }
   stage('Confirm Deploy to production') {
     steps {
       timeout(time: 60, unit: 'SECONDS') {
         input(message: 'Okay to Deploy?', ok: 'Let\'s Do it!')
       }
     }
   }
   stage('Deploy to Production') {
     steps {
       echo "Deploying to production..."
     }
   }
  }
  post {
   success {
     echo "Build succeeded!"
   }
   failure {
     echo "Build failed!"
   }
 }
}
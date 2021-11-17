pipeline {
  agent any

  stages {
    stage('Test') {
      steps {
        sh './mvnw test'
      }
    }

    stage('Build') {
      steps {
      	sh './mvnw package -DskipTests'
      }
    }

    stage('Code Analysis'){
      steps {
        sh './mvnw jacoco:report'
        // sh './mvnw jacoco:check'
      }	
    }
  }

  post {
    always {
      echo 'DONE'
      junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
      jacoco( 
        execPattern: 'target/*.exec',
        classPattern: 'target/classes',
        sourcePattern: 'src/main/java',
        exclusionPattern: 'src/test*'
      )
    }

    success {
      echo 'SUCCESS'
    }

    failure {
      echo 'FAILURE'
      // mail body: '<b>Job Failed</b>',
      //   from: '',
      //   mimeType: 'text/html',
      //   replyTo: '',
      //   subject: "JOB FAILURE: ${env.JOB_NAME} - #${env.BUILD_NUMBER}", 
      //   to: ''; 
      //  
    }
  }
}

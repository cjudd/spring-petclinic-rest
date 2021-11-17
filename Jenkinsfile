pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
      	sh './mvnw package -DskipTests'
      }
    }

    stage('Test') {
      steps {
        sh './mvnw test'
      }
    }

    stage('Code Quality'){
      steps {
        sh './mvnw jacoco:report'
      }	
    }

    stage('Release') {
      steps {
        echo 'Release ...'
      }
    }

    stage('Deploy'){
      steps {
        echo 'Deploy ...'
      }	
    }

  }

  post {
    always {
      echo 'DONE'
      junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
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

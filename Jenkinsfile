pipeline {
  agent any

  stages {
    stage('Build Artifact - Maven') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }
        }

    stage('Unit Tests - JUnit and Jacoco') {
        steps {
           sh "mvn test"
        }
        post {
           always {
             junit 'target/surefire-reports/*.xml'
             jacoco excePattern: 'target/jacoco.exec'              
            } 
        }
       }           
  
    stage('Docker Build and Push') {
        steps {
            sh 'printenv'
            sh 'docker build -t mega2/numeric-app:""$GIT_COMMIT"".'
            sh 'docker push mega2/numeric-app:""$GIT_COMMIT""'
           }
    }
  }    
}

 
           
    
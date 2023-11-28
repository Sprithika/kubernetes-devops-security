pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
        } 
      stage('Unit Test cases') {
            steps{
                sh "mvn test"
            }
            post {
              always{
                junit "targets/surefire-reports/*.xml"
                jacoco execPattern: "target/jacoco.exec"
              } 
            }  
       }
    }
}

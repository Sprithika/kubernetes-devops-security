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
                junit "target/surefire-reports/*.xml"
                jacoco execPattern: "target/jacoco.exec"
              } 
            }  
       }
      stage('Docker Build and Push') {
          steps{
            
            sh 'docker build -t prithika246/numeric-apps:""$GIT_COMMIT"" .'
            sh "docker login -u ${hub-un} -p ${hub-pass}"
            sh 'docker push prithika246/numeric-apps:""$GIT_COMMIT"" '
            sh ' docker logout'
          }  
      }  
    }
}

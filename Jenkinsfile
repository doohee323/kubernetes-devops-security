pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
      }   
      stage('Unit test') {
            steps {
              sh "mvn test"
            }
      }          
      stage('Docker build and Push') {
            steps {
                withKubeConfig([credentialsId: 'docker-hub']) {
                  sh "printenv"
                  sh 'docker build -t doohee323/numeric-app:""$GIT_COMMIT"" .'
                  sh 'docker push doohee323/numeric-app:""$GIT_COMMIT""'
                }        
            }
      }          

    }
}
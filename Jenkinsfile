pipeline {
  agent any
    tools{
      maven 'M2_HOME'
          }
   stages {
    stage('Git checkout') {
      steps {
         echo 'This is for cloning the gitrepo'
         git branch: 'master', url: 'https://github.com/kouser123/star-agile-banking-finance.git'
                          }
            }
    stage('Create a Package') {
      steps {
         echo 'This will create a package using maven'
         sh 'mvn package'
                             }
            }
     stage('Publish the HTML Reports') {
      steps {
          publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/finance-me/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                        }
            }
      stage('Create a Docker image from the Package finance-me.jar file') {
      steps {
        sh 'docker build -t samad12/insure-me-app:2.0 .'
                    }
            }
      stage('Login to Dockerhub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerlogin', passwordVariable: 'dockerpass', usernameVariable: 'dockeruser')]) {
        sh 'docker login -u ${dockeruser} -p ${dockerpass}'
                                                                    }
                                }
            }
     stage('Push the Docker image') {
      steps {
        sh 'docker push samad12/insure-me-app:2.0'
                               }
            }
   }

}

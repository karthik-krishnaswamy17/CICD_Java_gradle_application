pipeline{
    agent any
    stages{
        
        stage("Sonar Checks"){
            // agent {
            //     docker {
            //         image 'openjdk:11'
            //     }
            // }
            steps{
                script{
                  withSonarQubeEnv(credentialsId: 'sonar-token') {
                  sh 'chmod +x gradlew'
                  sh './gradlew sonarqube'
                 }
                 timeout(time: 5, unit: 'MINUTE') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
                

                }
                
            }
            
        }
    }
   
 post {
  always {
    cleanWs()
    dir("${env.WORKSPACE}@tmp") {
      deleteDir()
    }
    dir("${env.WORKSPACE}@*@tmp") {
      deleteDir()
    }
    dir("${env.WORKSPACE}@script") {
      deleteDir()
    }
    dir("${env.WORKSPACE}@script@tmp") {
      deleteDir()
    }
  }
}


}
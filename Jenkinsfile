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
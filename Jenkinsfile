pipeline{
    agent any
    environment{
      version="${env.BUILD_ID}"
    }
    stages{
        
        // stage("Sonar Checks"){
        //     // agent {
        //     //     docker {
        //     //         image 'openjdk:11'
        //     //     }
        //     // }
        //     steps{
        //         script{
        //           withSonarQubeEnv(credentialsId: 'sonar-token') {
        //           sh 'chmod +x gradlew'
        //           sh './gradlew sonarqube'
        //          }
        //          timeout(time: 5, unit: 'MINUTES') {
        //               def qg = waitForQualityGate()
        //               if (qg.status != 'OK') {
        //                    error "Pipeline aborted due to quality gate failure: ${qg.status}"
        //               }
        //             }
                

        //         }
                
        //     }
            
        // }

        stage("Dcoekr Build and Docker Push"){
          steps{
            script{
              withCredentials([string(credentialsId: 'nexus-user', variable: 'password')]) {
                sh '''
                 docker build -t nexusweb:8083/myjava-app:${version} .
                 docker login -u admin -p $password nexusweb:8083
                 docker push nexusweb:8083/myjava-app:${version}
                 docker rmi nexusweb:8083/myjava-app:${version}
                '''
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
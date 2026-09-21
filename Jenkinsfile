pipeline {
     agent any

   stages {
     stage('Chekout') {
       steps {
           checkout scm
       }
   }
    stage('build') {
       steps {
           script {
         dockerimage = docker.build("notifier:latest" , ".")
  
      }
   }
 }
   stage('Start container') {
       steps {
          script {
        sh 'docker run -d --name notifier-test -e ENV=test notifier:latest'
      }
    }
  }

   stage('Waiting 5 sec') {
       steps {
         sh 'sleep 5'
  }
}

  stage('Docker-filter') {
      steps {
       sh 'docker ps --filter "name=notifier-test" | grep notifier-test || exit 1'
    }
  }
}

   post {
      always {
         sh 'docker stop notifier-test || true'
         sh 'docker rm notifier-test || true'
     }
   }
}
  



   



currentBuild.displayName = "train-schedule-#" + currentBuild.number
pipeline {
  agent any 
  stages {
    stage ('Build'){
       steps {
         echo "Running Build Automation"
         sh 'pwd'
         sh 'sudo chmod +x gradlew'
         sh './gradlew build --no-daemon'
         archiveArtifacts artifacts: 'dist/trainSchedule.zip'
         sh './gradlew npm_start'
       }
    }
  }
}

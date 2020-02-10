pipeline {
  agent any 
  stages {
    stage ('Build'){
       steps {
         echo "Running Build Automation"
         sudo chmod +x gradlew
         sh './gradlew build --no-daemon'
         archiveArtifacts artifacts: 'dist/trainSchedule.zip'
       }
    }
  }
}

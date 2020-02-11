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
       }
    }
    stage ('DeploytoStaging') {
         when {
            branch 'master'
         }
         steps {
           withCredentials([usernamePassword(credentialID: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
             sshPublisher (
               failOnError: true, 
               continueOnError: false,
               publishers: [
                 sshPublisherDesc (
                   configName: 'staging',
                   sshCredentials: [
                     username: "deploy",
                     encryptedPassphrase: "jenkins"
                   ],
                   transfers: [
                     sshTransfer (
                       sourceFiles: 'dist/trainschedule.zip',
                       removePrefix: 'dist/',
                       remoteDirectory: '/tmp',
                       execCommand: 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule/* && unzip /tmp/trainschedule.zip -d /opt/train-schedule && sudo /usr/bin/systemctl start train-schedule'
                     )
                   ]
                 )
               ]
             )
           }
         }
    }
  }
}

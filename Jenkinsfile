pipeline {
	agent any
	tools {
        maven 'Maven'
    }
	stages {
		stage('Maven Installing the project ...') {
			steps {
				echo 'Now Maven is Installing'
				sh 'mvn clean install'
				script{
					committerEmail = sh (script: 'git --no-pager show -s --format=\'%ae\'',returnStdout: true).trim()
                    echo "The last commit was written by ${committerEmail}."
				}
			}
		}
	}
	post {
		always{
			echo "This will always run"
		}
		success {
			echo "This will run only if successful"
			office365ConnectorSend message: "CUSTOM MESSAGE STARTS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' ; The last commit was written by '${committerEmail}' ; CUSTOM MESSAGE ENDS", status:"SUCCESS", webhookUrl: "https://outlook.office.com/webhook/68d5ec6e-d483-4552-9312-42f3c5eb41de@dd02d1e4-d2a8-4628-92c8-1f4b5de6419b/JenkinsCI/b647544711594310ab17b8a8afbd246c/7dda7b5a-c806-446c-901d-2a379174dde9"
		}
		failure{
			echo "This will run only if failed"
			office365ConnectorSend message: "CUSTOM MESSAGE STARTS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' ; The last commit was written by '${committerEmail}' ; CUSTOM MESSAGE ENDS", status:"FAILED", webhookUrl: "https://outlook.office.com/webhook/68d5ec6e-d483-4552-9312-42f3c5eb41de@dd02d1e4-d2a8-4628-92c8-1f4b5de6419b/JenkinsCI/b647544711594310ab17b8a8afbd246c/7dda7b5a-c806-446c-901d-2a379174dde9"
		}
		unstable {
		  echo "This will run only if the run was marked as unstable"
		 }
		 changed {
		  sh 'echo "This will run only if the state of the Pipeline has changed"'
		}
	}
}

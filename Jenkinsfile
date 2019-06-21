node{
	stage('SCM Checkout'){
		git branch: 'slacknotification', url: 'https://github.com/jamesAdhikari/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-dev']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@3.91.180.24:/opt/tomcat9/webapps/'
		}
	}
	stage('Slack Notification'){
	slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkins', color: '#439FE0', message: 'New Build deployed', teamDomain: 'intelycore4', tokenCredentialId: 'slack-secret'
	}

}

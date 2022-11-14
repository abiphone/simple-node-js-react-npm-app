pipeline {
	agent {
		docker {
			image 'composer:latest'
		}
	}
	stages {
//             stage ('Checkout') {
// steps {
// git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
// }
// }
		stage('Build') {
			steps {
				sh 'composer install'
			}
		}
		stage('Test') {
			steps {
                sh './vendor/bin/phpunit tests'
            }
		}
        stage('Code Quality Check via SonarQube') {
steps {
script {
def scannerHome = tool 'ss';
withSonarQubeEnv('ss') {
sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=pp -Dsonar.sources=."
}
}
}
}
	}
    post {
always {
recordIssues enabledForFailure: true, tool: sonarQube()
}
}
}
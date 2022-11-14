pipeline {
	agent {
		docker {
			image 'composer:latest'
		}
	}
	stages {
		stage('Build') {
			steps {
				sh 'composer install'
			}
		}
                    stage ('Checkout') {
steps {
git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
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
def scannerHome = tool 'ughhuj';
withSonarQubeEnv('ss') {
sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=gg -Dsonar.sources=."
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
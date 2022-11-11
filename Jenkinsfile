pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/danieltannn/JenkinsDependencyCheckTest.git'
			}
		}
		stage('OWASP Dependency-Check') {
			steps {
				nodejs(nodeJSInstallationName: 'nodejs') {
					dependencyCheck(additionalArguments: '''
						--format XML \
						--format HTML \
						--suppression suppression.xml \
						--prettyPrint \
						--out .
					''',
					odcInstallation: 'dependency-check')
				}
			}
			post {
				success {
					dependencyCheckPublisher pattern: 'dependency-check-report.xml'
				}
			}
		}
	}
}

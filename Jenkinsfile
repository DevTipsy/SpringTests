pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    sh "echo réussit"
                }
            }
        }
        
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        
        stage('Install') {
            steps {
                sh "mvn install"
            }
        }

		post {
		always {
			echo "build terminé"
		}
		success {
			echo "success de toutes les étapes"
		}
		failure {
		mail to :"productowner@test.fr", subject: "Echec build", body : "verifie les tests..."
		}
	}  
    }
}

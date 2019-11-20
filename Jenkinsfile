pipeline {
    agent any

    stages {
        stage('Testing Environment') {
            steps {
                    sh 'mvn test -Dtest=ControllerAndServiceSuite'
			sh 'mvn test -Dtest=IntegrationSuite'
                }
            }
        stage('Build') {
            steps {
		sh 'mvn package -DskipTests'
		sh 'docker build -t="iestmj/simple-project:latest" .'
                }
            }
        stage('Deploy') {
            steps {
		sh 'docker push iestmj/simple-project:latest'
            }
        }
    

stage('Testing') {
            when {
                expression {
                        env.BRANCH_NAME!='master' && 'developer'
                }
        }
            steps {
                echo "testing"
            }
        }

      stage('Staging') {
        when {
                expression {
                        env.BRANCH_NAME=='developer' && 'master'
                }
        }
            steps {
                echo "staging"
            }
        }

      stage('Production') {
	when {
		expression {
			env.BRANCH_NAME=='master'
		}
	}
            steps {
                echo "production"
            }
        }
}
}

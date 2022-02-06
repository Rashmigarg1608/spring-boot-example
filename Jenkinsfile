pipeline {
    agent{
            label "linux"
        }
        tools {
            maven 'maven'
            jdk 'jdk 11'
        }
    stages {
                stage("building"){
            steps{
                sh "mvn compile"
		 
            }
                }

        stage('Testing') {
            steps {
                echo 'Testing the application...'
                sh "mvn clean test"
            }
        }
    }
    post {
        success{
        echo "Testing stage successful"
        }
        failure{
        echo "Testing stage failed"
        }
    }
}

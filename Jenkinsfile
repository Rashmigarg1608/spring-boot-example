pipeline {
    agent any 
        tools {
            maven 'Maven 3.8.4'
            //jdk 'jdk 11'
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

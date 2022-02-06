pipeline{
    agent{
        label "linux"
    }
    tools { 
        maven 'Maven 3.8.4' 
        jdk 'jdk 9.0.4'
    }
    stages{
	    
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
    post{
        always{
            mail to: 'rashmi.garg@knoldus.com',
			subject: "Pipeline: ${currentBuild.fullDisplayName} is ${currentBuild.currentResult}",
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
        }
        success{
            echo "Pipeline executed successfully.."
        }
        failure{
            echo "Pipeline execution failed.."
        }
    }
}

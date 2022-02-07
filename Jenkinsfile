pipeline
{
    agent  any 
    tools
    {
        maven 'Maven 3.8.4'
       // jdk 'jdk 11'
    }
    options
    {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
    }
    stages
    {
        stage("Cleanup")
        {
            steps
            {
                sh 'mvn clean test '
            }
        }
        
        stage("Test")
        {
            steps
            {
                sh 'mvn clean test'
            }
        }
        stage("Package")
        {
            steps
            {
                sh 'mvn  clean package'
            }
        }
    }
    post
    {
       always{
            mail to: 'garg.rashmi1608@gmail.com',
			subject: "Pipeline: ${currentBuild.fullDisplayName} is ${currentBuild.currentResult}",
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
        }
         success{
            sh 'echo "--------------------------Deploying------------------------------"'
            
        }
    }
}
        

 

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
            sshPublisher(publishers: [sshPublisherDesc(configName: 'production', transfers: [sshTransfer(cleanRemote: true, excludes: '', execCommand: '''cd product/target
java -jar .jar &''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'product', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '/.jar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
        }
    }
}
        

 

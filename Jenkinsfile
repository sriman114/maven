pipeline
{
    agent any
    stages
    {
        stage("continuous Download")
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
            
        }
        stage("continuous Build")
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage("continuous Deploy")
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'eab2c7e2-749f-4214-8273-a658df9885bc', path: '', url: 'http://172.31.10.253:8080')], contextPath: 'testingapp', war: '**/*.war'
            }
        }
        stage("Continuous Testing")
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/Declerativepipeline1/testing.jar'
                
            }
        }
        stage("Continuous delivery")
        {
            steps
            {
                input message: 'Need approval from DM!', submitter: 'Raghav'
                deploy adapters: [tomcat9(credentialsId: 'eab2c7e2-749f-4214-8273-a658df9885bc', path: '', url: 'http://172.31.10.52:8080')], contextPath: 'prod', war: '**/*.war'
            }
        }
    }
}

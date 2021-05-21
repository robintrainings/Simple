pipeline
{
    agent
    {
        node { label 'Jenkins9037StaticAgentWindows' }
    }
    options
    {
        timeout(time: 5, unit: 'HOURS') 
    }
    environment
    {
        sourceFolder = "src"
    }
    stages
    {
        stage('Build')
        {
            when { branch 'master' }
            steps
            {
                dir("${sourceFolder}")
                {
                    bat 'javac -version'
                    bat 'md bin'
                    bat 'javac -d bin -g:none -cp .\\lib\\* .\\src\\com\\continental\\DataHandling\\*.java .\\src\\com\\continental\\IntegrationTest\\*.java .\\src\\com\\continental\\*.java'
                }
            }
        }
        stage('IntegrationTests')
        {
            when { branch 'master' }
            steps            
            {
                dir("${sourceFolder}")
                {
                    echo 'Running SAPMES Test Suite'
                    bat '"%JAVA_HOME%\\bin\\java" -cp ".\\bin;%JAVA_HOME%\\jre\\lib\\rt.jar;.\\lib\\ojdbc6.jar;.\\lib\\jdom-2.0.6.jar;.\\lib\\jaxen-1.1.6.jar;.\\lib\\jsch-0.1.54.jar;.\\lib\\junit-jupiter-api-5.3.2.jar;.\\lib\\junit-jupiter-engine-5.3.2.jar;.\\lib\\junit-jupiter-migrationsupport-5.3.2.jar;.\\lib\\junit-jupiter-params-5.3.2.jar;.\\lib\\junit-platform-commons-1.3.2.jar;.\\lib\\junit-platform-console-1.3.2.jar;.\\lib\\junit-platform-console-standalone-1.3.2.jar;.\\lib\\junit-platform-engine-1.3.2.jar;.\\lib\\junit-platform-launcher-1.3.2.jar;.\\lib\\junit-platform-runner-1.3.2.jar;.\\lib\\junit-platform-suite-api-1.3.2.jar;.\\lib\\junit-platform-surefire-provider-1.3.2.jar;.\\lib\\junit-vintage-engine-5.3.2.jar" com.continental.SapmesTestSuite'
                }
            }
        }
    }
    post
    {
        always
        { 
            //Cleanup
            echo 'Start Cleanup...'
            //Remove git repository
            cleanWs()
        }
    }
}

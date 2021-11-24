def builderDocker
def CommitHash

pipeline {
    agent any 

    parameters {
        booleanParam(name: 'RunTest', defaultValue: true, description: 'Toggle this value for testing')
        choice(name: 'CICD', choices: ['CI', 'CICD'], description: 'pick CI / CI and CD')
        
    }
    stages {    
        stage('Run Testing') {
            steps{
                script {
                    sh 'echo passed'
                }
            }
        }

        stage('Test') {
            steps {
                dir('/Users/Nopal/Downloads/ci-samples-master'){
                    bat 'docker run -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -browserType="Chrome" -retry=0 -statusDelay=15 -testSuitePath="Test Suites/TS_RegressionTest"'
                }
            }
        }

    }
}
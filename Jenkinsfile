pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                dir('/var/jenkins_home/Katalon_Studio_Engine_Linux_64-8.2.0'){
                    sh './katalonc -noSplash -runMode=console -projectPath="/var/jenkins_home/test/test.prj" -retry=0 -testSuiteCollectionPath="Test Suites/try to integrate test suite collection" --config -proxy.auth.option=NO_PROXY -proxy.system.option=NO_PROXY -proxy.system.applyToDesiredCapabilities=true'
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true
            junit 'Reports/**/JUnit_Report.xml'
        }
    }
}
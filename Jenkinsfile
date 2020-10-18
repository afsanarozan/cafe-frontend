
def builderDocker
def CommitHash

pipeline {
    agent any 

    parameters {
        booleanParam(name: 'RunTest', defaultValue: true, description: 'Toggle this value for testing')
        
    }
    stages {

        stage('build Project') {
            steps{
                nodejs("node12") {
                    sh 'yarn install'
                }
            }
        }

        stage('ansible') {
            when {
                expression {
                    BRANCH_NAME == "dev"
                }
            }
            steps{
               script {
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: 'ansible',
                                verbose: false,
                                transfers: [
                                    sshTransfer(
                                        execCommand: 'cd ansible; ansible-playbook -i hosts advance-server.yml',
                                        execTimeout: 120000,
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }

        stage('ansible') {
            when {
                expression {
                    BRANCH_NAME == "master"
                }
            }
            steps{
               script {
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: 'ansible',
                                verbose: false,
                                transfers: [
                                    sshTransfer(
                                        execCommand: 'cd ansible; ansible-playbook -i hosts docker.yml',
                                        execTimeout: 120000,
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }

        // stage('Run Testing') {
        //     when {
        //         expression {
        //             params.RunTest
        //         }
        //     }
        //     steps{
        //         script {    
        //             builderDocker.inside{
        //                 sh 'echo passed ${BRANCH_NAME}'
        //             }
        //         }
        //     }
        // }

        // stage('Push Image') {
        //     when {
        //         expression {
        //             params.RunTest
        //         }
        //     }
        //     steps{
        //         script {    
        //             builderDocker.push("${env.GIT_BRANCH}")
        //         }
        //     }
        // }
        // stage('Deploy to production') {
        //     when {
        //         expression {
        //             BRANCH_NAME == "master"
        //         }
        //     }
        //     steps{
        //        script {
        //             sshPublisher(
        //                 publishers: [
        //                     sshPublisherDesc(
        //                         configName: 'production',
        //                         verbose: false,
        //                         transfers: [
        //                             sshTransfer(
        //                                 execCommand: 'docker pull 32480/frontend:prod; docker kill frontend;docker run -d --rm -p 8080:80 --name frontend 32480/frontend:prod',
        //                                 execTimeout: 120000,
        //                             )
        //                         ]
        //                     )
        //                 ]
        //             )
        //         }
        //     }
        // }

        // stage('Deploy to Development') {
        //     when {
        //         expression {
        //             BRANCH_NAME == "dev"
        //         }
        //     }
        //     steps{
        //        script {
        //             sshPublisher(
        //                 publishers: [
        //                     sshPublisherDesc(
        //                         configName: 'Developmen',
        //                         verbose: false,
        //                         transfers: [
        //                             sshTransfer(
        //                                 execCommand: 'docker pull 32480/frontend:dev; docker kill frontend;docker run -d --rm -p 8080:80 --name frontend 32480/frontend:dev',
        //                                 execTimeout: 120000,
        //                             )
        //                         ]
        //                     )
        //                 ]
        //             )
        //         }
        //     }
        // }
    }
}

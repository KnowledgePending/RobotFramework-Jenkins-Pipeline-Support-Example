pipeline {
    agent any
    // Run every 15 minutes
    triggers {
        cron('H/15 * * * *')
    }
    stages{
        stage('Prep'){
            steps{
                node('slave-01') {
                    cleanWs()
                }
            }
        }
        stage('Test') {
            steps{
                node('slave-01') {
                        sh '''
                                # replace repo with the source of your tests
                                git clone <repo>.git
                                cd ./<repo_name>
                                robot --outputdir reports <other_robot_options> <test_dir>
                        '''
                }
            }
        }
    }
    post {
        always {
            node('slave-01') {
                step([
                    $class : 'RobotPublisher',
                    outputPath : '<repo_name>/reports/',
                    outputFileName : "*.xml",
                    disableArchiveOutput : false,
                    passThreshold : 100,
                    unstableThreshold: 95.0,
                    otherFiles : "*.png",
                ])
                archiveArtifacts artifacts: '<repo_name>/reports/*.*'
                cleanWs()
            }

        }
    }
}

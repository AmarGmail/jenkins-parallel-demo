/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    options {
        timestamps()
    }

    stages{
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh '''
                echo "Build Started"
                sleep 5
                echo "Build Completed"
                '''
            }
        }

        //Parallel stage started
        stage('Testing') {
            parallel {
                stage('Unit Tests') {
                    /* groovylint-disable-next-line NestedBlockDepth */
                    steps {
                        echo 'Running Unit Tests...'
                        sh '''
                        echo "Unit Test Started"
                        sleep 5
                        echo "Unit Test Completed"
                        '''
                    }
                }
                stage('Security Tests') {
                    /* groovylint-disable-next-line NestedBlockDepth */
                    steps {
                        echo 'Running Security Tests...'
                        sh '''
                        echo "Security Test Started"
                        sleep 5
                        echo "Security Test Completed"
                        '''
                    }
                }
                stage('Integration Tests'){
                    /* groovylint-disable-next-line NestedBlockDepth */
                    steps {
                        echo 'Running Integration Tests...'
                        sh '''
                        echo "Integration Test Started"
                        sleep 5
                        echo "Integration Test Completed"
                        '''
                    }
                }
            }
        }
        //Out of Parallel stage

        stage('Code Tests') {
            steps {
                echo 'Running Code Tests...'
                sh '''
                echo "Code Test started"
                sleep 5
                echo "Code Test Completed"
                '''
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                echo "Deployment Started"
                sleep 5
                echo "Deployment Completed"
                '''
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            sh '''
            echo "Cleanup started"
            sleep 5
            echo "Cleanup completed"
            '''
//            echo '---archiving artifacts---'
//            archiveArtifacts artifacts: '**/target/*.jar, **/dist/**/*', 
//                allowEmptyArchive: true

        }
        success {
            echo '----Build Successful----'
            echo "Build ${env.BUILD_NUMBER} completed successfully"
            // send github notify
            githubNotify(
                status: 'SUCCESS',
                description: "✅ Build #${env.BUILD_NUMBER} succeeded",
                context: "Jenkins CI",
                credentialsId: 'github-pat'
            )
        }
        failure {
            echo '----Build Failed----'
            echo "Build ${env.BUILD_NUMBER} failed!"
            //send failure to github
            githubNotify(
                status: 'FAILURE',
                description: "❌ Build #${env.BUILD_NUMBER} failed",
                context: "Jenkins CI",
                credentialsId: "github-pat"
                )
        }
        aborted {
            echo "--- Build Aborted---"
            githubNotify(
                status: "ERROR",
                description: "⚠️ Build #${env.BUILD_NUMBER} was aborted",
                context: 'Jenkins CI',
                credentialsId: 'github-pat'
                )
        }
    }
}

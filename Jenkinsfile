pipeline {
    agent any
    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'feature/meghna_jenkins_pl2',
                    url: 'https://github.com/expertszen/java-batch-job-example.git'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Run Application') {
            steps {
                bat 'java -cp target/java-batch-job-example-1.0-SNAPSHOT.jar com.expertszen.BatchJobApp'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Post Build Notification') {
            steps {
                script {
                    if (currentBuild.currentResult == 'SUCCESS') {
                        emailext(
                            subject: "SUCCESS: Jenkins Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
                            body: """
                                The Jenkins job '${env.JOB_NAME}' has completed successfully.

                                Build Number: ${env.BUILD_NUMBER}
                                Status: SUCCESS
                                Build URL: ${env.BUILD_URL}
                            """,
                            to: 'expertszen@gmail.com'
                        )
                    } else if (currentBuild.currentResult == 'FAILURE') {
                        emailext(
                            subject: "FAILURE: Jenkins Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
                            body: """
                                The Jenkins job '${env.JOB_NAME}' has FAILED.

                                Build Number: ${env.BUILD_NUMBER}
                                Status: FAILURE
                                Check logs here: ${env.BUILD_URL}
                            """,
                            to: 'expertszen@gmail.com'
                        )
                    }
                }
            }
    }
    }
}

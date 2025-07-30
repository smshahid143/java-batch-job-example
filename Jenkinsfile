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
        stage('Build & Run Batch Job') {
            steps {
                bat 'mvn clean install'
                bat 'java -cp target\\java-batch-job-example-1.0-SNAPSHOT.jar com.expertszen.BatchJobApp'
            }
        }
    }
    post {
        always {
            emailext(
                subject: "Job 2 Execution: ${currentBuild.currentResult}",
                body: "Batch job completed with status: ${currentBuild.currentResult}\nCheck logs at ${env.BUILD_URL}",
                to: 'lead.engineer@example.com'
            )
        }
    }
}

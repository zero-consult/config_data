pipeline {
    agent any
    stages {
        stage('Undeploy previous services') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sh "docker compose -f compose.yaml down"
                }
            }
        }
        stage('Deploy services') {
            steps {
                withCredentials([string(credentialsId: 'PostgresPassword', variable: 'POSTGRES_PASSWORD')]) {
                    sh "docker compose -f compose.yaml up &"
                }
            }
        }
    }
}
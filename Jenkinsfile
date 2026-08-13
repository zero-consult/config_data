pipeline {
    agent any
    stages {
        stage('Undeploy previous services') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    script {
                        docker.withRegistry('http://nexus:8081', 'Nexus') {
                            sh(returnStdout: false, script: "docker compose -f compose.yaml down")
                        }
                    }
                }
            }
        }
        stage('Deploy services') {
            steps {
                withCredentials([
                    string(credentialsId: 'PostgresPassword', variable: 'POSTGRES_PASSWORD'),
                    string(credentialsId: 'JwtSecretKey', variable: 'JWT_SECRET_KEY')]) {
                    script {
                        docker.withRegistry('http://nexus:8081', 'Nexus') {
                            sh(returnStdout: false, script: "docker compose -f compose.yaml up -d")
                        }
                    }
                }
            }
        }
    }
}
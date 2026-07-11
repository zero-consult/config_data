pipeline {
    agent any
    stages {
        stage('Deploy services') {
            steps {
                [
                    $class: 'DockerComposeBuilder',
                    dockerComposeFile: 'compose.yaml',
                    option: [
                        $class: 'StartService',
                        scale: 1,
                        service: 'zero_consult'
                    ],
                    useCustomDockerComposeFile: true
                ]
            }
        }
    }
}
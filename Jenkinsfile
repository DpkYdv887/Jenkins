pipeline {
    agent any

    stages {
        stage("Clone Repository") {
            steps {
                // Updated Git repo details
                git branch: 'main', credentialsId: 'e34582d6-e3e4-4c7f-9618-97e21e76f896', url: 'https://github.com/DpkYdv887/Jenkins.git'
            }
        }

        stage("Verifying Tooling") {
            steps {
                sh '''
                    docker version
                    docker info
                    docker compose version
                    curl --version
                    jq --version
                '''
            }
        }

        stage("Prune Docker Data") {
            steps {
                sh 'docker system prune -a --volumes -f'
            }
        }

        stage("Start Container") {
            steps {
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose ps'
            }
        }

        stage("Check Response") {
            steps {
                sh 'curl http://localhost'
            }
        }
    }
}

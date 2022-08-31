pipeline {
    agent {label "linux"}

    stages {
        stage('Hello') {
            steps {
                script {
                    sh """
                    mvn --version
                    docker info
                    gradle --version
                    """
                }
            }
        }
    }
}
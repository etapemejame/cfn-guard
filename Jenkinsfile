// Pipeline starts here

pipeline {
    agent {any}
    options {
        timestamps()
        ansiColor('xterm')
    }
    stages 
    {
        stage('Hello')
        {
            steps
            {
                sh '''
                echo Hello World. This is a test Jenkins Pipeline

                '''
            }
        }
    }
}
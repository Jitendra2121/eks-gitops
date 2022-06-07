pipeline {
    agent any
    parameters {
        string(name: 'BUILD_NUMBER_X', description: 'enter env value')
    }
    stages {
        stage('Env Pass Successful') {
            steps {
                script{
                    echo "${params.BUILD_NUMBER_X}"
                }
            }
        }
    }
}

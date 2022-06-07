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
                    echo 'Build Number: ' + params.BUILD_NUMBER_X
                echo "Succefully push the version ${params.BUILD_NUMBER_X} of the python flask app"
                }
            }
        }

        stage('Clone SCM') {
            steps {
                script{
                    checkout scm
                }
            }
        }

        stage('Update GIT Repo for GitOps') {
            steps {
              script {
                catchError(buildResult: 'Success', stageResult: 'Failure') {
                    withCredentials([usernamePassword(credentialsId: 'Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {              
                sh 'sudo git config --global user.name "Jitendra2121"'
                sh 'sudo git config --global user.email atkj2102@gmail.com'
                sh 'sudo cat /home/ubuntu/final/eks-gitops/deployment.yml'
                sh "sudo sed -i 's+jeetdocker21/test.*+jeetdocker21/test:${BUILD_NUMBER_X}+g' /home/ubuntu/final/eks-gitops/deployment.yaml"
                sh 'sudo cat /home/ubuntu/final/eks-gitops/deployment.yml'
                sh 'sudo git add .'
                sh 'sudo git commit -m "Changed the Deployment file container image version to: ${BUILD_NUMBER_X}"'
                sh 'sudo git push https://${GIT_USERNAME}:{GIT_PASSWORD}@github.com/${GIT_USERNAME}/eks-gitops.git HEAD:main'

                echo 'Build Number: ' + env.BUILD_NUMBER_X
                echo "Succefully build the version ${BUILD_NUMBER_X} of the python flask app using GitOps."
                    }
                }
            }
        }
    }
  }
}

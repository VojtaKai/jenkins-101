// pipeline {
//     agent any

//     triggers {
//         pollSCM('H/6 * * * *')
//     }

//     stages {
//         stage('Hello') {
//             steps {
//                 echo "Hello, it's me. I was wondering if after all the years you'd like to meet. --Adele"
//             }
//         }
//     }

//     post {
//         always {
//             echo "This text is visible on every run!"
//         }

//         success {
//             echo "This text is only visible when the pipeline ran successfully"
//         }

//         failure {
//             echo "Failure! Check logs."
//         }
//     }
// }

pipeline {
    agent { 
        node {
            label 'docker-agent-python'
        }
    }

    triggers {
        pollSCM 'H * * * *'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install -r myapp/requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                source venv/bin/activate
                cd myapp
                python3 hello.py
                python3 hello.py --name=Vojta
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
        stage('Final Message') {
            steps {
                sh '''
                ./jenkins/scripts/final_message.sh
                '''
            }
        }
    }

    post {
        always {
            echo "This text is visible on every run!"
        }

        success {
            echo "This text is only visible when the pipeline ran successfully"
        }

        failure {
            echo "Failure! Check logs."
        }
    }
}
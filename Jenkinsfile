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
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
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
}
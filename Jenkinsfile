pipeline {
    agent { 
        node {
            label 'docker_agent_alpine'
            }
      }
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                set -xe

                # Switch to root user
                su -c "apt-get update && apt-get install -y python3 python3-pip && apt install -y python3.11-venv"
                cd myapp
                python3 -m venv venv
                ls
                source venv/bin/activate
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
                python3 hello.py --name=Brad
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
    }
}
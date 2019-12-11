pipeline {
    agent any
    stages {
        stage('Prepare') {
            steps {
                sh 'php --version'
                sh 'rm -rf *'
                sh 'git clone https://github.com/pmbibe/Docker'
                sh "chmod -R 755 Demo_jenkins"
            }
        }
        stage('Test') {
            steps {
                echo "--------------------Test Stage---------------------"
                sh "cd Demo_jenkins && pwd && ant"
            }
        }
        stage('Deploy') {
            steps {
                echo "--------------------Deploy Stage---------------------"
                junit 'Demo_jenkins/build/logs/*.xml'
                sh "pwd"
                sh "Demo_jenkins/Deploy.sh"
            }
        }
        stage('RollBack') {
            steps {
                echo "--------------------Deploy Stage---------------------"
                input(message: 'Do you like Java?', ok: 'Yes', 
                        parameters: [booleanParam(defaultValue: true, 
                        description: 'If you like Java, just push the button',name: 'Yes?')])
            }
        }
    }
}

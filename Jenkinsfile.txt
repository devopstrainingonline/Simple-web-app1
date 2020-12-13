pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/devopstrainingonline/Simple-web-app1.git'
            }
        }
		stage('Unit Test') {
            steps {
                echo 'Unit Test'
            }
        }
		stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }
		stage('Deploy') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'f2f4251e-adab-4e74-9770-7c7d59d1fbe1', path: '', url: 'http://localhost:9595')], contextPath: '/simple-web-app', war: '**/*.war'
            }
        }
		stage('E-Mail Notification') {
            steps {
                echo 'E-Mail Notification'
            }
        }
		
    }
}

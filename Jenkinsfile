pipeline {
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        /*
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/sarkarp24/simple-java-project1.git'
            }
        }
        */
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                //sh 'mvn clean'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            /*
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
            */
        }
        stage('Deliver') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat_user', path: '', url: 'http://54.191.84.186:8080/')], contextPath: 'web-app', war: '**/*.war'
            }
        }
    }
}
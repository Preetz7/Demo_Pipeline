pipeline {
    agent any

    tools {
        maven "Maven"
    }

    stages {
        
        stage('Check_version') {
            steps {
                bat 'mvn --version'
        }
        }
        
        stage('Path') {
            steps {
                git 'https://github.com/Preetz7/Demo_Pipeline.git'
        }
        }
        
        stage('Check_branch') {
                when
                {   
                    branch 'master'
                }
                steps {
                       echo 'The default branch is master'
                       input('Do you want to proceed?')
                }
        }
        
        stage('Build') {
            steps {
                bat 'mvn clean install package -DskipTests'
        }
        }
        stage('Deploy') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat_credentials', path: '', url: 'http://localhost:9090/')], contextPath: 'target', war: '**/*.war'
        }
        }
        
    }
}

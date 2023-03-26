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
                steps {
                script {
                    if (env.BRANCH_NAME == 'master') {
                        echo 'The default branch is master'
                    }  
                    else {
                        echo 'The default branch is not master'
                    }
                 }
            }
        }
        
        stage('Build') {
            steps {
                bat 'mvn clean install package -DskipTests'
        }
        }
        
        stage('Consent') {
            input {
                    message "Need to deploy on Tomcat?"
                    ok "Yes"
            }
            steps {
                    echo 'Deploying on Tomcat'  
            }
        }
        stage('Deploy') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat_credentials', path: '', url: 'http://localhost:9090/')], contextPath: 'target', war: '**/*.war'
            }
        }  
    }
    post{
        always { 
            echo 'I will always say Hello again!'
        }
        failure{
            echo 'Failure'
        }
        success{
            echo 'Successs'
        }
    }
}

pipeline { 
    agent any
    
    tools {
        maven 'Maven' // Must match Jenkins Global Tool Configuration 
        jdk 'JDK'     // Configure this as JDK 21 in Jenkins
    }
    
    stages {
        stage('Checkout') { 
            steps {
                checkout scm
            }
        }
        
        stage('Build') { 
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn clean compile'
                    } else {
                        bat 'mvn clean compile'
                    }
                }
            }
        }
        
        stage('Test') { 
            steps {
                script {
                    if (isUnix()) { 
                        sh 'mvn test'
                    } else {
                        bat 'mvn test'
                    }
                }
            }
        }
    } // Closes stages
    
    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    } // Closes post
} // Closes pipeline (This was the missing one!)

pipeline {
    agent {
        node{
         label 'maven'   
        }
    }

Environment {
    PATH = /opt/apache-maven-3.9.9/bin:$PATH
}
    stages {
        stage('Build1.1') {
            steps {
                sh 'mvn clean deploy'
            }
           
        }
    }
}

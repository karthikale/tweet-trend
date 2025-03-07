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
        stage('Build') {
            steps {
                sh 'mvn clean deploy'
            }
           
        }
    }
}

    pipeline {
        agent {
            node{
            label 'maven'   
            }
        }

    environment {
        PATH = "/opt/apache-maven-3.9.9/bin:${PATH}"
    }    
        stages {
            stage("build-1.2") {
                steps {
                    sh 'mvn clean deploy'
                }
                
    
        }
    }

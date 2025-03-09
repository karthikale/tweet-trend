def registry = 'https://trialya7rhd.jfrog.io'

pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    environment {
        PATH = "/opt/apache-maven-3.9.9/bin:${PATH}"
    }

    stages {
        stage("build-1.4") {
            steps {
                echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "----------- build completed ----------"
            }
        }

        stage("Jar Publish") {
            steps {
                script {
                    echo '<--------------- Jar Publish Started --------------->'
                    
                    def server = Artifactory.newServer(url:registry+"/artifactory", credentialsId:"jfrog-token")
                    def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}"
                    def uploadSpec = """{
                        "files": [
                            {
                                "pattern": "jarstaging/(*)",
                                "target": "libs-release-local/com/valaxy/demo-workshop/2.1.4/{1}",  // Target repository and path
                                "flat": "false",
                                "props": "${properties}",
                                "exclusions": ["*.sha1", "*.md5"]
                            }
                        ]
                    }"""
                    
                    def buildInfo = server.upload(uploadSpec)
                    buildInfo.env.collect()
                    server.publishBuildInfo(buildInfo)  // Moved inside script block
                }

                echo '<--------------- Jar Publish Ended --------------->'  // Moved inside steps block
            }
        }
    }
}

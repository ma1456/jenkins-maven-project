pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ma1456/jenkins-maven-project.git']])
            }
        }
       stage ("build Jar") {
            steps {
                sh "/opt/maven/bin/mvn -f hello-app/pom.xml clean package"
            }
        }
	stage('Upload'){
            steps{
                rtUpload (
                 serverId:"jfrog" ,
                  spec: '''{
                   "files": [
                      {
                      "pattern": "*.jar",
                      "target": "maven-repo-local/"
                      }
                            ]
                           }''',
                        )
               }
         }
	stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "jfrog"
                 )
                }
            }
       
        }
  }

pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
<<<<<<< HEAD
                sh 'mvn -f hello-app/pom.xml -B -DskipTests clean install'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.jar'
                }
=======
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ma1456/jenkins-maven-project.git']])
>>>>>>> fd8fb94c64ead1ce77b2d82b2cb5f4cbd9a6e32b
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

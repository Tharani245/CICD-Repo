pipeline {
    agent any 
       
    stages {
        stage("git clone") {
            steps {
                git branch: 'master',url: 'https://github.com/Tharani245/CICD-Repo.git'
            }
        }
        stage("build") {
            steps {
                sh "mvn clean install"
            }
        }
        stage("Test and Code Coverage") {
            steps {
                // mnv test
                junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
                // junit '**/test-reports/*.xml'
                jacoco ()
            }
        }
        stage("code analysis") {
            steps {
                script {
                    withSonarQubeEnv('sonarqube-9.7') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
        stage("Upload in Artifactory") {
            steps {
                rtUpload (
                    serverId: 'jfrog-artifact',
                    spec: '''{
                        "files": [
                            {
                                "pattern": "*.war",
                                "target": "demomavenrepo"
                            }
                        ]
                    }''',
                    buildName: 'firstbuild',
                    buildNumber: '1'
                )
            }
        }
        stage("download from artifactory") {
            steps {
                rtDownload (
                    serverId: 'jfrog-artifact',
                    spec: '''{
                        "files": [
                            {
                                "pattern": "*.war",
                                "target": "artifacts"
                            }
                        ]
                    }''',
                )
            }
        }
    }
}

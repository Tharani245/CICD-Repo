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
        stage("build") {
            steps {
                sh "mvn clean install"
            }
        }
        stage("package") {
            steps {
                sh "mvn package"
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
                rtupload (
                    serverId:"jfrog-artifact",
                    spec:''' {
                        "files": [
                            {
                                "pattern"="*.war",
                                "target"="demomavenrepo"
                            }
                        ]
                    }''',

                )
            }
        }
    }
}

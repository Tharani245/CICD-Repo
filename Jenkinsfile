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
    }
}

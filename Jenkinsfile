pipeline {
    agent { label 'GOL'}
    stages {
        stage('scm') {
            steps {
                 git branch: 'master' url: 'https://github.com/muralivts9/game-of-life.git'
            }
           
        }
        stage('build') {
            steps {
                sh 'mvn package'
            }
        }

    }
    post {
        success {
         archive '**/*.war'
         junit '**/TEST-*.xml'   
        }
    }
}
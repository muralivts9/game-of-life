pipeline {
    agent { label 'GOL'}
    triggers {
        cron ('H * * * *')
        pollSCM ('* * * * *')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'build with master')
    }
    stages {
        stage('scm') {
            steps {
                 git branch: "${perams.BRANCH}", url: 'https://github.com/muralivts9/game-of-life.git'
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
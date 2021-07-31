pipeline {
    agent { label 'GOL'}
    triggers {
        cron ('H * * * *')
        pollSCM ('* * * * *')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to build')
    }
    stages {
        stage('scm') {
            steps {
                 git branch: "${params.BRANCH}", url: 'https://github.com/muralivts9/game-of-life.git'
            }
           
        }
        stage('build') {
            steps {
                echo env.GIT_URL
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
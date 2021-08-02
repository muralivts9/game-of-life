pipeline {
    agent { label 'GOL'}
    triggers {
        cron ('H * * * *')
        pollSCM ('* * * * *')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to build')
        choice(name: 'GOAL', choices: ['package', 'clean package', 'install', 'deploy'], description: 'maven goals')
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        retry(2)
    }
    stages {
        stage('scm') {
            steps {
                mail subject: 'BUILD Strated'+env.BUILD_ID, to: 'murali.cool999@gmail.com', from: 'murali.chirumamilla99@gmail.com', body: 'status'
                 git branch: "${params.BRANCH}", url: 'https://github.com/muralivts9/game-of-life.git'
            }
           
        }
        stage ('build the packages') {
            steps {
	           sh 'mvn package'
            }  
        }
        stage('build') {
            steps {
                echo env.GIT_URL
                sh "mvn ${params.GOAL}"
            }
        }
        stage('SonarQube analysis') {
            // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
              withSonarQubeEnv('SONAR-6.7.4') {
             // requires SonarQube Scanner for Maven 3.2+
              sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
            }
        }

        
        
    }
    post {
        success {
         archive '**/*.war'
         junit '**/TEST-*.xml'
         mail subject: 'BUILD Completed Successfull'+env.BUILD_ID, to: 'murali.cool999@gmail.com', from: 'murali.chirumamilla99@gmail.com', body: 'success'   
        }
        failure {
            mail subject: 'BUILD Faild'+env.BUILD_ID+ 'URL is'+env.BUILD_URL, to: 'murali.cool999@gmail.com', from: 'murali.chirumamilla99@gmail.com', body: 'faild'
        }
    }
}
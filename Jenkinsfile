node('GOL') {
    stage('SCM') {
        git 'https://github.com/muralivts9/game-of-life.git'
    }
    stage('buid') {
        sh 'mvn clean package'
    }
    stage('postbuild') {
        junit '**/TEST- *.xml'
        archive '**/*.war'
    }
}
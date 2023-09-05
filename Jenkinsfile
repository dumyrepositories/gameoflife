pipeline {
    agent { label 'JDK8-11-17' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/dumyrepositories/gameoflife.git',
                branch: 'master'
            }
        }
        stage('build') {
            tools {
                jdk 'JDK-8'
            }
            steps {
                sh 'mvn package'
            }
        }
        stage('postbuild') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war',
                                 onlyIfSuccessful: yes
                junit testResults: '**/surefire-reports/TEST-*.xml',
                      allowEmptyResults: no
            }
        }
    }
}
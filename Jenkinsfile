pipeline {
    agent { label 'GRADLE_8' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Prakashlearning/spring-petclinic-1.git',
                    branch: 'declarative'
            }
        }
        stage('gradle build') {
            tools {
                jdk 'JDK_11'
            }
            steps {
                sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH"
            }
        }  
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/*.jar',
                                 allowEmptyArchive: true,
                                 fingerprint: true,
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}
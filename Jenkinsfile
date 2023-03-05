pipeline {
    agent { label 'GRADLE_8' }
    tools { jdk 'JDK_17'
            gradle 'GRADLE_7' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Prakashlearning/spring-petclinic-1.git',
                    branch: 'declarative'
            }
        }
        stage('gradle build') {
            steps {
                sh 'export PATH="/usr/lib/jvm/java-1.17.0-openjdk-amd64/bin:$PATH" && gradle build'
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
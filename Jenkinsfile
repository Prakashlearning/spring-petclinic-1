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
                jdk 'JDK_17'
            }
            steps {
                sh '/opt/gradle/gradle-7.4.2/bin/gradle build'
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
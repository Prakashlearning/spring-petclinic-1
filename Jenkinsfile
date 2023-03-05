pipeline {
    agent { label 'GRADLE_7' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Prakashlearning/spring-petclinic-1.git',
                    branch: 'declarative'
            }
        }
        stage('gradle build') {
            steps {
                sh "/opt/gradle/gradle-7.4.2/gradle build"
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
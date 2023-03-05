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
            tools{
                jdk 'JDK_17'
            }
            steps {
                sh 'export PATH="/opt/gradle/gradle-7.4.2/bin:$PATH" && gradle build'
            }
        }  
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/*.txt',
                                 allowEmptyArchive: true,
                                 fingerprint: true,
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}
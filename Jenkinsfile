pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Doc') {
            steps {
                sh 'mvn surefire-report:report'
                sh 'mvn javadoc:jar'
            }
        }

        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        
        stage('Test report') {
            steps {
                sh 'mvn test --fail-never'
            }
        }
        
    }
    
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}

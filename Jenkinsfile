pipeline {
    agent any

    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('install sonar') {
            steps {
                    sonar: {
                        sh "mvn sonar:sonar -Dsonar.host.url=${env.SONARQUBE_HOST}"
                    }
            }
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                    step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])
                }
            }
        }
        stage('deploy') {
            steps {
                sh "mvn deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL}"
            }
        }
    }
}

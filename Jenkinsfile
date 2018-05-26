pipeline {
    agent any

    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

        stage('install sonar') {
            steps {
                        sh "mvn sonar:sonar -Dsonar.host.url=${env.SONARQUBE_HOST}"
                    }
            }

        stage('deploy') {
            steps {
                sh "mvn deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL}"
            }
        }
    }
pipeline {
    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
    agent any

    stages {
        stage("checkout") {
            steps {
                git 'https://github.com/Chinku-code/maven-test.git'
            }
        }

        stage("compile") {
            steps {
                sh 'mvn compile'
            }
        }

        stage("test") {
            steps {
                sh 'mvn test'
            }
        }

        stage("package") {
            steps {
                sh 'mvn clean package'
                sh "mv target/*.jar target/myweb.jar"
            }
        }

        stage("backup") {  // FIX: Stage name must be in quotes
            steps {
                nexusArtifactUploader(
                    credentialsId: 'nexus1',
                    nexusVersion: 'nexus2',
                    protocol: 'http',
                    nexusUrl: '34.46.133.185:8081/repository/maven-releases/',
                    repository: 'maven-releases',
                    groupId: 'com.idream',
                    version: '1.0',
                    artifacts: [
                        [artifactId: 'myweb', classifier: '', file: 'target/myweb.jar', type: 'jar']
                    ]
                )
            }
        }
    }
}

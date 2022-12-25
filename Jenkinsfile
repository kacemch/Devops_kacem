
pipeline {
    agent any
    stages {
        stage('Cloning project') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: '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', url: 'https://github.com/kacemch/Devops_kacem.git'
                echo "-------------------Clone Stage Done ------------------------------- "
            }
        }
        stage("clean){
            steps {
                script {
                    sh "mvn -Dmaven.test.failure.ignore=true clean"
                }
            }
        }
        stage("compile") {
            steps {
                script {
                    sh "mvn -Dmaven.test.failure.ignore=true compile"
                }
            }
        }
        stage("test") {
            steps {
                script {
                    sh "mvn -Dmaven.test.failure.ignore=true test"
                }
            }
        }
        stage("build") {
            steps {
                script {
                    sh "mvn -Dmaven.test.failure.ignore=true clean package"
                }
            }
        }
        stage('deploy to nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'tpAchatProject', classifier: '', file: 'target/tpAchatProject-1.0.jar', type: 'jar']], credentialsId: 'c4e9649d-5f97-4f24-9ced-184dbd641c2d', groupId: 'com.esprit.examen', nexusUrl: '192.168.56.12:8081/repository/maven-releases/', nexusVersion: 'nexus3', protocol: 'http', repository: 'nexusdeploymentrepo', version: '1.0'
            }
        }
        
    }    

}


pipeline {
    agent any
    stages {
        stage('Cloning the project') {
            steps {
                // clone from git and test trigger
                git branch: 'main', credentialsId: '15abb24f-d15c-4109-b679-858a4caa469f', url: 'https://github.com/kacemch/Devops_kacem.git'
                echo "-------------------Clone Stage Done ------------------------------- "
            }
        }
        stage("clean"){
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
        stage('deploy to nexus repo') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'tpAchatProject', classifier: '', file: 'target/tpAchatProject-1.0.jar', type: 'jar']], credentialsId: '3bd88c32-6fe9-4038-a7db-8d97af16bd65', groupId: 'com.esprit.examen', nexusUrl: '192.168.56.12:8081/repository/maven-releases/', nexusVersion: 'nexus3', protocol: 'http', repository: 'nexusdeploymentrepo', version: '1.0'
            }
        }
        
    }    

}

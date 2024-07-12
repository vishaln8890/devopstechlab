pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'java17'
    }
    stages {
        stage('git pull') {
            steps {
                echo "Download git code"
                git branch: 'main', url: 'https://github.com/vishaln8890/devopstechlab.git'
            }
        }
        stage('build') {
            steps {
                echo "Doing build"
                sh 'mvn clean package'
            }
        }
        stage('Copy Artifacts') {
            steps {
                echo "Archive Artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('build other job') {
            steps {
                echo "Build other job"
                build wait: false, job: 'deploy-to-dev-pipeline'
            }
        }
    }
}

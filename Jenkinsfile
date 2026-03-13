pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat '''
                    @echo off
                    echo Build stage started
                    if not exist build mkdir build
                    copy /Y update.txt build\update.txt >nul
                    echo Build stage completed
                '''
            }
        }

        stage('Test') {
            steps {
                bat '''
                    @echo off
                    echo Test stage started
                    if exist build\update.txt (
                        echo Test stage completed
                    ) else (
                        echo build\\update.txt not found
                        exit /b 1
                    )
                '''
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    @echo off
                    echo Deploy stage started
                    if not exist deploy mkdir deploy
                    copy /Y build\update.txt deploy\update.txt >nul
                    echo Deploy stage completed
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'build/**, deploy/**', fingerprint: true
        }
    }
}

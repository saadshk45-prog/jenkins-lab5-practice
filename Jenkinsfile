pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build started'
            }
        }

        stage('Test') {
            steps {
                bat '''
                    if exist index.html (
                        echo TEST PASSED
                    ) else (
                        echo TEST FAILED
                        exit /b 1
                    )
                '''
            }
        }

        stage('Docker Build') {
            steps {
                bat '''
                    set "PATH=C:\\Users\\Admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"
                    docker build -t jenkins-lab5-practice .
                '''
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    set "PATH=C:\\Users\\Admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"

                    docker stop jenkins-lab5-practice-container 2>nul
                    docker rm jenkins-lab5-practice-container 2>nul

                    docker run -d --name jenkins-lab5-practice-container -p 8083:80 jenkins-lab5-practice
                '''
            }
        }
    }
}

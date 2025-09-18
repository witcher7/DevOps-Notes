pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                cleanWs()
                echo 'Building a new laptop ...'
                sh '''
                    mkdir -p build
                    touch build/computer.txt
                    echo "Mainboard" >> build/computer.txt
                    cat build/computer.txt
                    echo "Display" >> build/computer.txt
                    cat build/computer.txt
                    echo "Keyboard" >> build/computer.txt
                    cat build/computer.txt
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'build/**'
        }
    }
}

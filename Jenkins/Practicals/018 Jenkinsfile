pipeline {
    agent any

    environment {
        BUILD_FILE_NAME = 'laptop.txt'
    }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                echo 'Building a new laptop ...'
                sh '''
                    echo $BUILD_FILE_NAME
                    mkdir -p build
                    echo "Mainboard" >> build/$BUILD_FILE_NAME
                    cat build/$BUILD_FILE_NAME
                    echo "Display" >> build/$BUILD_FILE_NAME
                    cat build/$BUILD_FILE_NAME
                    echo "Keyboard" >> build/$BUILD_FILE_NAME
                    cat build/$BUILD_FILE_NAME
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the new laptop ...'
                sh '''
                    test -f build/$BUILD_FILE_NAME
                    grep "Mainboard" build/$BUILD_FILE_NAME
                    grep "Display" build/$BUILD_FILE_NAME
                    grep "Keyboard" build/$BUILD_FILE_NAME
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

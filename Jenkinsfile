pipeline {
    agent any  // Uses any available agent (Windows in your case)

    environment {
        PROJECT_DIR = 'Plant-Disease-Classifier-main'
    }

    options {
        skipDefaultCheckout(true)  // Prevent Jenkins from checking out code automatically
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Manually checkout the 'master' branch
                git branch: 'master', url: 'https://github.com/devanshsengar04/plant-disease.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                script {
                    def isWindows = isUnix() ? false : true
                    if (isWindows) {
                        def pythonExists = bat(script: 'where python', returnStatus: true) == 0
                        if (!pythonExists) {
                            bat '''
                                echo Python not found. Installing...
                                choco install python -y
                            '''
                        }
                        bat 'python --version'
                    } else {
                        echo 'This script is for Windows agents only.'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                dir(PROJECT_DIR) {
                    script {
                        def isWindows = isUnix() ? false : true
                        if (isWindows) {
                            bat '''
                                python -m venv venv
                                call venv\\Scripts\\activate
                                pip install --upgrade pip
                                pip install -r requirements.txt
                            '''
                        } else {
                            echo 'This script is for Windows agents only.'
                        }
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                dir(PROJECT_DIR) {
                    script {
                        def isWindows = isUnix() ? false : true
                        if (isWindows) {
                            bat '''
                                call venv\\Scripts\\activate
                                python -m pytest tests/
                            '''
                        } else {
                            echo 'This script is for Windows agents only.'
                        }
                    }
                }
            }
        }

        stage('Update Visitor Count') {
            steps {
                script {
                    def isWindows = isUnix() ? false : true
                    if (isWindows) {
                        bat '''
                            echo Updating visitor count...
                            curl -X POST http://localhost:8501/api/update_visitor_count
                        '''
                    } else {
                        echo 'This script is for Windows agents only.'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}

pipeline {
    agent any 
    tools {nodejs "NodeJS"}

    stages {

        stage ("Clonar o Hub de Leitura Integrado") {
            steps {
                bat 'if exist hub-de-leitura-integrado rmdir /s /q hub-de-leitura-integrado'
                bat 'git clone --depth 1 https://github.com/Cassiana-Lima/hub-de-leitura-integrado.git'
            }
        }

         stage ("Instalar dependencias do projeto") {
            steps {
                dir('hub-de-leitura-integrado') {
                    bat '''
                     call npm install
                     start /B npm start
                     '''
                }
            }
        }

        stage ("Clonar o projeto de teste") {
            steps {
                bat 'if exist hub-de-leitura-teste-ui2 rmdir /s /q hub-de-leitura-teste-ui2'
                bat 'git clone --depth 1 https://github.com/Cassiana-Lima/hub-de-leitura-teste-ui2.git'
            }
        }

        stage ("Instalar dependencias dos projetos de teste") {
            steps {
                dir('hub-de-leitura-teste-ui2') {
                    bat 'call npm install'
                }
            }
        }

        stage ("Executar os testes automatizados") {
            steps {
                dir ('hub-de-leitura-teste-ui2') {
                    bat 'call npm test'                
                }
            }
        }
    }

    post {
        always {
            dir ('hub-de-leitura-teste-ui2') {
                archiveArtifacts artifacts: 'cypress/screenshots/**/*.*, cypress/videos/**/*.*', allowEmptyArchive: true
                 allure includeProperties: false, jdk: '', results: [[path: 'allure-report']]
            } 
            
            bat 'taskkill /F /IM node.exe || exit 0'
        }
    }
 }
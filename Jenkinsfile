pipeline {
    agent any 
    tools {nodejs "NodeJS"}

    stages {

        stage ("Clonar o Hub de Leitura Integrado") {
            steps {
                bat 'if exist hub-de-leitura-integrado rmdir /s /q hub-de-leitura-integrado'
                bat 'git clone https://github.com/Cassiana-Lima/hub-de-leitura-integrado.git'
            }
        }

         stage ("Instalar dependencias do projeto") {
            steps {
                dir('hub-de-leitura-integrado') {
                    bat 'npm install'
                    bat 'npm start'
                }
            }
        }
    }
 }
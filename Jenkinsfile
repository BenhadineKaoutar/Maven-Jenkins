pipeline {
    agent any
    
    stages {
         stage('build') {
            steps {
                bat "mvn compiler:compile"
                echo 'Building..'
            }
            post{
            success{ bat "echo ' Projet compilé avec succes '"}
            failure{bat " echo ' Erreur lors de la compilation du projet '" }
            }
        }
        stage('test') {
            steps {
                bat 'mvn test'
                echo 'Testing..'
            }
            post{
            always {junit 'target/surefire-reports/*.xml'}
            }
        }
        stage('couverture') {
            steps {
                bat "mvn cobertura:cobertura -Dcobertura.report.format=xml"
            }
            post{
            always
            {cobertura coberturaReportFile: '**/target/site/cobertura/coverage.xml'}
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

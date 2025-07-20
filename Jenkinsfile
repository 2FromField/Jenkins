pipeline {
    agent any  // Ce pipeline peut être exécuté sur n'importe quel agent

    environment {
        GIT_REPO = 'https://github.com/ton-utilisateur/ton-repository.git' // URL du dépôt
        BRANCH = 'main' // Branche du dépôt Git à utiliser
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Cloner le dépôt Git
                    git branch: "${BRANCH}", url: "${GIT_REPO}"
                }
            }
        }

        stage('Check .sh File') {
            steps {
                script {
                    // Vérifie si le fichier .sh existe et est exécutable
                    def shFile = 'script.sh'
                    if (fileExists(shFile)) {
                        echo "Le fichier ${shFile} existe"
                    } else {
                        error "Le fichier ${shFile} n'existe pas dans le dépôt"
                    }
                    
                    // Tester si le fichier est exécutable
                    sh "chmod +x ${shFile}"
                    
                    // Optionnellement, tu peux ajouter des tests de syntaxe sur le fichier .sh
                    sh "bash -n ${shFile}"
                }
            }
        }

        stage('Run Script') {
            steps {
                script {
                    // Exécuter le fichier .sh
                    sh './script.sh'
                }
            }
        }

        stage('Commit and Push Changes') {
            steps {
                script {
                    // Ajouter, commit et push les changements sur le dépôt Git
                    sh 'git add .'
                    sh 'git commit -m "Mise à jour après l'exécution du script" || echo "Aucun changement à pousser"'
                    sh 'git push origin ${BRANCH}'
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline exécuté avec succès"
        }
        failure {
            echo "Le pipeline a échoué"
        }
    }
}
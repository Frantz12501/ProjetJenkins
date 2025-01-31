pipeline {
    // Définir l'agent global
    agent any

    // Définir les variables d'environnement
    environment {
        CONTAINER_ID = 'cfff5667dbb47d05f8cde17c613b4f91446c817573467e9463b6f68787e271ac' // ID du conteneur sera stocké ici
        SUM_PY_PATH = './sum.py' // Chemin vers le script sum.py sur la machine locale
        DIR_PATH = '.' // Chemin vers le répertoire contenant le Dockerfile
    }

    stages {
        // Étape 1 : Construction de l'image Docker
        stage('Build Docker Image') {

            steps {
                echo 'Building the Docker image...'
                echo "${DIR_PATH}"
                bat '''
                docker build -t python-sum .
                '''
            }
        }

        // Étape 2 : Exécution du conteneur Docker
        stage('Run Docker Container') {
            steps {
                echo 'Running the Docker container...'
                script {
                    // Lancer le conteneur en mode détaché
                    // CONTAINER_ID = bat(
                    //     script: "docker run -dit python-sum",
                    //     returnStdout: true
                    // ).trim()
                    env.CONTAINER_ID_RUN = bat(script: 'docker run -dit python-sum', returnStdout: true).trim()
                    echo "Container ID: ${env.CONTAINER_ID_RUN}"
                    echo "Container ID: ${CONTAINER_ID_RUN}"
                }
            }
        }

    }
}

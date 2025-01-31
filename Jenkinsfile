pipeline {
<<<<<<< HEAD
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Construire l'image Docker à partir du Dockerfile
                    docker.build("sum-python")
=======
    agent any // Utiliser n'importe quel agent disponible

    environment {
        // Variables d'environnement
        CONTAINER_ID = '32642581b89605c1857a1f029988cc3878018dcc5051d049cab55ee0072b842c' // Stockera l'ID du conteneur Docker
        SUM_PY_PATH = 'sum.py' // Chemin vers le fichier sum.py
        DIR_PATH = '.' // Chemin vers le répertoire contenant le Dockerfile
        TEST_FILE_PATH = 'test_variables.txt' // Chemin vers le fichier de test
    }

    stages {
        // Étape 1 : Construire l'image Docker
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Construction de l'image Docker..."
                    sh "docker build -t sum-python ${DIR_PATH}"
>>>>>>> d7044f9 (bonjour)
                }
            }
        }

<<<<<<< HEAD
        stage('Run Docker Container') {
            steps {
                script {
                    // Exécuter le conteneur avec les arguments 5 et 10
                    docker.image("sum-python").run("5 10")
=======
        // Étape 2 : Exécuter le conteneur Docker
        stage('Run Docker Container') {
            steps {
                script {
                    echo "Exécution du conteneur Docker..."
                    CONTAINER_ID = sh(script: "docker run -d sum-python", returnStdout: true).trim()
                    echo "ID du conteneur : ${CONTAINER_ID}"
                }
            }
        }

        // Étape 3 : Tester le script Python
        stage('Test Script') {
            steps {
                script {
                    echo "Test du script sum.py avec les valeurs du fichier test_variables.txt..."

                    // Lire le fichier de test
                    def testVariables = readFile(TEST_FILE_PATH).trim().split('\n')

                    // Tester chaque paire de valeurs
                    testVariables.each { line ->
                        def (arg1, arg2) = line.split()
                        echo "Test avec les arguments : ${arg1} et ${arg2}"

                        // Exécuter le script dans le conteneur
                        def result = sh(script: "docker exec ${CONTAINER_ID} python /app/sum.py ${arg1} ${arg2}", returnStdout: true).trim()
                        echo "Résultat : ${result}"
                    }
                }
            }
        }

        // Étape 4 : Nettoyer
        stage('Cleanup') {
            steps {
                script {
                    echo "Arrêt et suppression du conteneur..."
                    sh "docker stop ${CONTAINER_ID}"
                    sh "docker rm ${CONTAINER_ID}"
>>>>>>> d7044f9 (bonjour)
                }
            }
        }
    }
}
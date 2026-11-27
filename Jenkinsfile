node {
    stage('Checkout') {
        checkout scm
    }
    stage('Outils') {
        sh 'java -version'
        sh 'mvn -v || echo "Maven n est pas installe sur ce serveur"'
    }
}

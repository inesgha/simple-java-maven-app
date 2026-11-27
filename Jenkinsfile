node {
    def jdkHome = tool name: 'JDK-21', type: 'jdk'
    def mvnHome = tool name: 'Maven-3.9.9', type: 'maven'
    withEnv(["JAVA_HOME=${jdkHome}", "PATH+JDK=${jdkHome}/bin", "PATH+MAVEN=${mvnHome}/bin"]) {
        stage('Checkout') {
            checkout scm
        }
        stage('Outils') {
            sh 'java -version'
            sh 'mvn -v'
        }
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn -B test'
        }
        stage('Execution') {
            sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
        }
        stage('Image') {
            sh "docker build -t minain/bibliotheque:${env.BUILD_NUMBER} ."
        }
        stage('Push') {
            withCredentials([string(credentialsId: 'docker_hub_pwd', variable: 'DOCKER_PWD')]) {
                sh 'echo "$DOCKER_PWD" | docker login -u minain --password-stdin'
            }
            sh "docker push minain/bibliotheque:${env.BUILD_NUMBER}"
        }
    }
}

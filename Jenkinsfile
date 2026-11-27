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
    }
}

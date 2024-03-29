node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("daresekulovski/kiii-jenkins")
    }
    stage('Push image') {
    withDockerRegistry([ credentialsId: "dockerhub", url: "https://index.docker.io/v1/" ]) {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
        }
    }
}

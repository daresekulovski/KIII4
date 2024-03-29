node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("daresekulovski/kiii-jenkins")
    }
    stage('Push image') {
    withCredentials([usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
        def registry_url = "registry.hub.docker.com/"
        bat "docker login -u $USER -p $PASSWORD ${registry_url}"
        docker.withRegistry("http://${registry_url}", "dockerhub") {
            // Push your image now
            bat "docker push daresekulovski/kiii-jenkins:latest"
            }
        }
    }
}

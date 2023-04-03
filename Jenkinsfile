node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
    stage('Build image') {
       app = docker.build("add5/kiii-lab4")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'kiii-dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}

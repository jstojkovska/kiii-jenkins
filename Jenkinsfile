node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("janastoj/kiii-jenkins") 
    }

    stage('Push image') {
        // Push само ако сме на 'dev' гранка
if (env.BRANCH_NAME == "dev") {
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
        app.push("${env.BRANCH_NAME}-latest")
    }
} else {
    echo "Skipping push step – not on 'dev' branch (current: ${env.BRANCH_NAME})"
}

    }
}

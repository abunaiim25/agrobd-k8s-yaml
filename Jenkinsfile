node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        withCredentials([
            gitUsernamePassword(credentialsId: 'naiim-github', gitToolName: 'Default')
        ]) {
            script {
                sh "git checkout main"
                sh "git config pull.rebase true"                
                sh "git pull"
                sh "git status"
                sh "sed -i 's+image:.*+image: ${params.DOCKER_TAG}+g' ./deployment/Deploy.yaml"               
                sh "cat ./deployment/Deploy.yaml"
                sh 'git config user.email "rayhan@ba-systems.com"'
                sh 'git config user.name "Abu Naiim"'
                sh "git add ."
                sh "git commit -m '${params.DOCKER_TAG}'"
                sh "git push"
            }
        }
    }
}

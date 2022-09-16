def secret = 'Jenkinskel4'
def server = 'jenkinss@103.174.114.178'
def directory = 'housy-frontend'
def branch = 'main'

pipeline{
    agent any
    stages{
        stage ('compose down &  pull'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker compose down
                    docker system prune -f
                    git pull origin ${branch}
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker build'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker compose build
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker up'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker compose up -d
                    exit
                    EOF"""
                }
            }

        }
	stage ('discord cuyy'){
            steps{
                echo 'Test to Discord'
		discordSend description: 'Berhasil', footer: '', image: '', link: '', result: '', scmWebUrl: '', thumbnail: '', title: '', webhookURL: 'https://discord.com/api/webhooks/1020154216347611157/AUzYJMHVQ5rRHG4VAW9ARfw076K3DyK3jybGDKB78T5QIssqTb5zurEzlwGw85QB8byH'
               }
            }
    }
}


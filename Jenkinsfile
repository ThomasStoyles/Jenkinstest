pipeline{
        agent any
        stages{
            stage('Clone'){
                steps{
                    sh "git clone https://gitlab.com/qacdevops/chaperootodo_client"
                }
            }
            stage('Install Docker'){
                steps{
                    sh " apt-get update"
                    sh " apt install curl -y"
                    sh "curl https://get.docker.com | sudo bash"
                    sh " usermod -aG docker (whoami)"
                }
            }
            
            stage('Install Docker-compose'){
                steps{
                    sh "sudo apt-get update"
                    sh "sudo apt install curl -y"
                    sh "version=(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r '.tag_name')"
                    sh "sudo curl -L https://github.com/docker/compose/releases/download/{version}/docker-compose-(uname -s)-(uname -m) -o /usr/local/bin/docker-compose"
                    sh "sudo chmod +x /usr/local/bin/docker-compose"
                    sh "docker-compose --version"
                }
            }
            
            stage('Deploy'){
                steps{
                    sh "sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d"
                }
            }
        }
}

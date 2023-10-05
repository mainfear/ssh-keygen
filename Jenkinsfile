pipeline {

agent any
    stages {
        stage('Create Ansible Inventory') {
            steps {
                sh 'echo "[web]\nserver1 ansible_host=192.168.1.101" > inventory.ini'
            }
        }
        stage('Upload to GitHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github_cred', usernameVariable: 'Username', passwordVariable: 'Password')]) {
                    sh 'git config --global user.email "example@mail.com"'
                    sh 'git config --global user.name "mainfear"'
                    sh 'git clone https://github.com/mainfear/ssh-keygen'
                    sh 'cd ./ssh-keygen'
                    sh 'git add inventory.ini'
                    sh 'git commit -m "Add Ansible inventory file"'
                    sh 'git remote add origin https://github.com/mainfear/ssh-keygen'
                    sh 'git push --set-upstream origin main'
                }
            }
        }
    }
}

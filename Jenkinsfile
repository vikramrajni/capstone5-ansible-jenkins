pipeline {   
  agent any
  environment {
    ANSIBLE_SERVER = "159.203.43.201"
  }
  stages {
    stage("copy files to ansible server") {
      steps {
        script {
          echo "copying all necessary files to ansible control node"
          sshagent(['Digital-Ocean']) {
            sh "scp -o StrictHostKeyChecking=no ansible/* root@${ANSIBLE_SERVER}:/root"

            withCredentials([sshUserPrivateKey(credentialsId: 'AWS-ansible2-pem', keyFileVariable: 'keyfile', usernameVariable: 'user')]) {
              sh 'scp $keyfile root@$ANSIBLE_SERVER:/root/ssh-key.pem'
            }
          }
        }
      }
    }
    stage ("execute ansible playbook") {
      steps {
        script {
          echo "calling ansible playbook to configure ec2 instances"
          def remote = [:]
          remote.name = "ansible-server"
          remote.host = ANSIBLE_SERVER
          remote.allowAnyHosts = true

          withCredentials([sshUserPrivateKey(credentialsId: 'Digital-Ocean', keyFileVariable: 'keyfile', usernameVariable: 'user')]) {
            remote.user = user
            remote.identityFile = keyfile
            // sshCommand remote: remote, command: "ls -l"
            sshScript remote: remote, script: "prepare-ansible-server.sh"
            sshCommand remote: remote, command: "ansible-playbook my-playbook.yaml"
          }
        }
      }
    }      
  }
} 

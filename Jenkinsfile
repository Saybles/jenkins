pipeline {
  agent any
  stages {
    stage('Run vagrant environment') {
      steps {
        sh 'vagrant box list'
        sh 'cd ~/dev/DevOps/Jenkins/vagrant_env && vagrant up "/jenkins-vm-[1-${machines_count}]/"'
      }
    }
    stage('Install Docker + run tomcat container') {
      steps {
        // sh 'sudo -i'
        // sh 'echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list'
        // sh 'exit'
        // sh 'sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367'
        // sh 'sudo apt update'
        // sh 'sudo apt install ansible'
        
        sh 'cd ~/dev/DevOps/Jenkins/ansible && ansible-galaxy install -p $(pwd)/roles nickjj.docker'
        sh 'whoami'
        sh 'cd ~/dev/DevOps/Jenkins/ansible && ansible-playbook docker_playbook.yml --vault-password-file=vault.txt --extra-vars "@secret"'
        
        sh 'docker pull tomcat'
        sh 'docker run -d --rm -p 8888:8080 tomcat:8.0'
      }
    }
  }
}
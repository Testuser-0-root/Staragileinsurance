node{
    stage('git checkout'){
        git 'https://github.com/Testuser-0-root/Staragileinsurance'
    }
   
    stage('build and package'){
        sh 'mvn clean package'
    }
    
    stage('selenium test'){
        sh 'mvn test'
    }
    
    stage('Docker build and images'){
        sh 'docker build -t testuser0root/test .'
        sh 'docker images'
    }
    
    stage('Docker login ') {
      withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
        sh "echo $PASS | docker login -u $USER --password-stdin"
     }
     }
   
    stage('Docker push ') {
     sh 'docker push testuser0root/test '
     }    
     stage('Deploy on ansible') {
    ansiblePlaybook become: true, credentialsId: 'anisble', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml', vaultTmpPath: ''
    
     }     
}

node{
    
    stage('checkout'){
        git 'https://github.com/surecode555/capstone-Insurance-project.git'
    }
    
    stage('maven build'){
        sh 'mvn clean package'
    }
    
    stage('containerize'){
       // sh 'docker build -t surecode555/insure-me:1.0 .'
    }
    
    stage('Release'){
         withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'dockerHubPwd')]) {
               //sh "docker login -u surecode555 -p ${dockerHubPwd}"
                //sh 'docker push surecode555/insure-me:1.0'
               }
    }
    
        stage('Deploy to Test')
        {

            ansiblePlaybook become: true, credentialsId: 'ansible-key1', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml', vaultTmpPath: ''
        }

        stage('checkout regression test source code'){
            git 'https://github.com/surecode555/capstone-project.git'
        }

        stage('build test script')
        {
            sh 'mvn clean package assembly:single'
        }

        stage('execute selenium test script')
        {
           sh 'java -jar target/my-app-test-0.0.1-SNAPSHOT-jar-with-dependencies.jar'
        }
         stage('code checkout')
        {
            git 'https://github.com/surecode555/capstone-Insurance-project.git'
        }
         stage('Deploy to Prod')
        {
            ansiblePlaybook become: true, credentialsId: 'ansible-key1', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-prod-server.yml', vaultTmpPath: ''
        }

    }

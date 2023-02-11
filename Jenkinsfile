
pipeline {
    agent {
        label "myage"
    }

environment
{
   DHC=credentials('dockerhub')
}
    stages {
        stage('git') {
            steps {
                checkout scm
            }
        }
        
        stage('rm') {
            steps {
              sh "ansible-playbook ap.yaml"
            }
        }        
        
        
        stage('build') {
            steps {
                sh 'docker build -t sab22/prg3:$BUILD_NUMBER .'
            }
        }        
        
        
        
        stage('login') {
            steps {
                sh 'echo $DHC_PSW | docker login -u $DHC_USR --password-stdin'
            }
        } 
        
        
        stage('push') {
            steps {
                sh 'docker push sab22/prg3:$BUILD_NUMBER'
            }
        }            
        
        stage('triget manf') {
            steps {
                sh 'docker push sab22/prg3:$BUILD_NUMBER'
            }
        }        
        
        
       stage('chnge') {
         steps{
             script{
               build job: 'ufst', parameters: [string(name: 'DOCKERTAG2', value: env.BUILD_NUMBER)]
             }
         }
    }             
        
        
        
        
    }
}


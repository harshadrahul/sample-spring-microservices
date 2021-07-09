pipeline {
agent {
label 'Build-server'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; mvn clean install " 
    }
}
            stage ('dockerbuild') 
{
    steps
    {
        sh "cd /home/ubuntu/jenkins/workspace/Jenkins-Pipeline-java-ms/account-service; sudo docker build -t account-service . " 
    }
}
    }
            stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; sudo  docker login -mk72-vision2020 "
        sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; sudo docker tag account-service mk72/account-service  "
        sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; sudo docker push mk72/account-service  "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node (' Ansible-server') {
             sh " sudo ansible-playbook /root/k8s.yaml"
   
    }
}
}
}  
}

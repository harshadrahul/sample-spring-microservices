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
       sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/$(Service_name) ; mvn clean install " 
    }
}

    stage ('Sonarqubw') {
        
        
       steps 
        {
            sh "sonar-scanner \-Dsonar.projectKey=java3 \ -Dsonar.sources=. \ -Dsonar.host.url=http://15.207.16.44:9000 \-Dsonar.login=1a9cf7a9c684b65c1782d581063b0bfb0d36f15b
     
        }
            stage ('dockerbuild') 
{
    steps
    {
        sh "cd /home/ubuntu/jenkins/workspace/Jenkins-Pipeline-java-ms/${Service_name}; sudo docker build -t account-service . " 
    }
}
    }
            stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/$(Service_name) ; sudo  docker login -mk72-vision2020 "
        sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/$(Service_name) ; sudo docker tag account-service mk72/$(Service_name)  "
        sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/$(Service_name) ; sudo docker push mk72/$(Service_name)  "
        
        
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

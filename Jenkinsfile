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
       sh "cd /home/ubuntu/jenkins/workspace/final_project/account-service ; mvn clean install " 
    }
}
            stage ('dockerbuild') 
{
    steps
    {
        sh "cd /home/ubuntu/jenkins/workspace/final_project/account-service; sudo docker build -t account-service . " 
    }
}
            stage ('dockerimagepush') 
{
    steps
    {
       sh "cd /home/ubuntu/jenkins/workspace/final_project/account-service ; sudo  docker login -u mk72 -p vision2020"
        sh "cd /home/ubuntu/jenkins/workspace/final_project/account-service ; sudo docker tag account-service mk72/account-service  "
        sh "cd /home/ubuntu/jenkins/workspace/final_project/account-service ; sudo docker push mk72/account-service  "
        
        
    }
}
    
}  
}

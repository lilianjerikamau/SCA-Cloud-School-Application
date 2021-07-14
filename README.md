# SCA-Cloud-School-Application
# Integrating github project with jenkins



## JENKINS LINK http://a66183f28757.ngrok.io/job/SCA%20Cloud%20School%20Application/
         ## username lilianjerikamau
        ## password linahjerry123.
        
        
        
## JENKINS PIPELINE SYNTAX USED FOR DEFINING JENKINSFILE
There are two types of Jenkins pipeline syntax used for defining your JenkinsFile.

1.Declarative
2.Scripted

## Declarative:

Declarative pipeline syntax offers an easy way to create pipelines. It contains a predefined hierarchy to create Jenkins pipelines. It gives you the ability to control all aspects of a pipeline execution in a simple, straight-forward manner.

## Example


pipeline {
    agent any
    stages {
        stage('Source') {
            steps { 
                echo 'Creating'
            }
        }
     stages {
        stage('Build') {
            steps { 
                echo 'Building'
            }
        }
      stages {
        stage('Deploy') {
            steps { 
                echo 'Deploying'
            }
        }   
    }
}

## Scripted:

Scripted Jenkins pipeline runs on the Jenkins master with the help of a lightweight executor. It uses very few resources to translate the pipeline into atomic commands. Both declarative and scripted syntax are different from each other and are defined totally differently.


 ## Example  
     
   node {
    stage('Source')
    {
        echo 'Creating'
    }
      stage('Build')
    {
        echo 'Building'
    }
      stage('Deploy')
    {
        echo 'Deploying'
    }
       }
       

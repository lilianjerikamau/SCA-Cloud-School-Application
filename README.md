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
    agent none 
    stages {
        stage(' Source') {
            agent { docker 'maven:3-alpine' } 
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
        stage('Build') {
            agent { docker 'openjdk:8-jre' } 
            steps {
                echo 'Hello, JDK'
                sh 'java -version'
            }
        }
        stage(' Source') {
            agent { docker 'maven:3-alpine' } 
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
    }
}
// Script //
    
  

## Scripted:

Scripted Jenkins pipeline runs on the Jenkins master with the help of a lightweight executor. It uses very few resources to translate the pipeline into atomic commands. Both declarative and scripted syntax are different from each other and are defined totally differently.


 ## Example 
 
node {
    stage('Source') {
        try {
            sh 'exit 1'
        }
        catch (exc) {
            echo 'Something failed, I should sound the klaxons!'
            throw
        }
     stage('Build') {
        try {
            sh 'exit 2'
        }
        catch (exc) {
            echo 'Something failed, I should sound the klaxons!'
            throw
        }
       stage('Deploy') {
        try {
            sh 'exit 3'
        }
        catch (exc) {
            echo 'Something failed, I should sound the klaxons!'
            throw
        }
    }
}
     

 
  
       

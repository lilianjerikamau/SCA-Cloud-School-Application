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

```java

pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git credentialsId: 'github', url: 'https://github.com/lilianjerikamau/SCA-Cloud-School-Application.git'
           }
          }
     stage("Maven Build"){
       steps{
            sh "mvn clean package"
            sh "mv target/*.war target/myweb.war"
             }
            }
     stage("deploy-dev"){
       steps{
          sshagent(['tomcat-dev1']) {
          sh """
          scp -o StrictHostKeyChecking=no target/myweb.war  
          ubuntu@yourip:/opt/tomcat/webapps/
          ssh ubuntu@yourip /opt/tomcat/bin/shutdown.sh
          ssh ubuntu@yourip /opt/tomcat/bin/startup.sh
           """
            }
          }
        }
      }
    }
```
    
  

## Scripted:

Scripted Jenkins pipeline runs on the Jenkins master with the help of a lightweight executor. It uses very few resources to translate the pipeline into atomic commands. Both declarative and scripted syntax are different from each other and are defined totally differently.


 ## Example 
 ```java
node {  
    stage('Git Checkout') { 
        git credentialsId: 'github', url: 'https://github.com/lilianjerikamau/SCA-Cloud-School-Application.git'
    }
    stage('Maven Build') { 
       buildInfo = rtGradle.run rootDir: "gradle-examples/4/gradle-example-ci-server/", buildFile: 'build.gradle', tasks: 'clean artifactoryPublish'
    }
    stage('deploy-dev') { 
      server.publishBuildInfo buildInfo
    }
}
  ```   

 
  
       

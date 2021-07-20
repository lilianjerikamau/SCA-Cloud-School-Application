# SCA-Cloud-School-Application
# Integrating github project with jenkins



## JENKINS LINK https://804318880022.ngrok.io/job/SCA%20Cloud%20School%20Application/
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
## Configuring GitHub with jenkins step by step
 

Step 1: go to your GitHub repository and click on ‘Settings’.
integrating jenkins and github

Step 2: Click on Webhooks and then click on ‘Add webhook’.

Step 3: In the ‘Payload URL’ field, paste your Jenkins environment URL. At the end of this URL add /github-webhook/. In the ‘Content type’ select: ‘application/json’ and leave the ‘Secret’ field empty.

Step 4: In the page ‘Which events would you like to trigger this webhook?’ choose ‘Let me select individual events.’ Then, check ‘Pull Requests’ and ‘Pushes’. At the end of this option, make sure that the ‘Active’ option is checked and click on ‘Add webhook’ 

Step 5: In Jenkins, click on ‘New Item’ to create a new project.

Step 6: Give your project a name, then choose ‘Freestyle project’ and finally, click on ‘OK’.

Step 7: Click on the ‘Source Code Management’ tab.

Step 8: Click on Git and paste your GitHub repository URL in the ‘Repository URL’ field

Step 9: Click on the ‘Build Triggers’ tab and then on the ‘GitHub hook trigger for GITScm polling’. Or, choose the trigger of your choice.Triggering the Jenkins Job to Run with Every Code Commit

Step 10: Click on the ‘Build’ tab, then click on ‘Add build step’ and choose ‘Execute shell’.

Step 12: Go back to your GitHub repository, edit the README.md file and commit the changes. We will now see how Jenkins ran the script after the commit

Step 13: Go back to your Jenkins project and you'll see that a new job was triggered automatically from the commit you made at the previous step. Click on the little arrow next to the job and choose ‘Console Output’.


 


 
  
       

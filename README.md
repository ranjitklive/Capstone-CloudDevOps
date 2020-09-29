## Udacity DevOps Capstone Project

The purpose is to apply the skills and knowledge developed throughout the Cloud DevOps Nanodegree program. These include:

* Working in AWS
* Using Jenkins to implement Continuous Integration and Continuous Deployment
* Building pipelines
* Working with CloudFormation to deploy clusters
* Building Kubernetes clusters
* Building Docker containers in pipelines

---
### Setting-up AWS infrastructure

For deploying infrastructure, execute the below script found inside cloudformation/ folder:

    sh ./create.sh CloudDevOpsCapstone network_and_eks.yml network_and_eks.json
    
Note: The creation of EKS cluster takes almost 10 minutes

### Setting your pipeline for lint, build and publish your docker image

Jenkins build pipeline is defined in `Jenkinsfile`. Also, before running the pipeline, we have to login to Docker.com for publishing blue/gree docker image.

### Blue Green deployment configuration setting in Kubernetes using Controllers and Service

1) Apply blue controller within blue-green/blue folder
    
    `kubectl apply -f blue-controller.json`
    
2) Apply green controller within blue-green/green folder
    
    `kubectl apply -f green-controller.json`
    
3) Deploy service within blue-green/ folder

    `kubectl apply -f blue-green-service.json`
    
   Then you can check the application deployed in the browser
    
4) For do a blue-green deployment update the section to **green** in blue-green-service.json file:

    "selector":{
          "app":"blue" 
        },

5) Deploy again the service

    `kubectl apply -f blue-green-service.json`
    
    We can see how each POD is updated to the green version incrementally
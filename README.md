# Capstone-DevOps-project

In this project we will apply the skills and knowledge which were developed throughout the Cloud DevOps Nanodegree program. These include:

Working in AWS

Using Jenkins to implement Continuous Integration and Continuous Deployment

Building pipelines

Working with Ansible and CloudFormation to deploy clusters

Building Kubernetes clusters

Building Docker containers in pipelines

We will develop a CI/CD pipeline for micro services applications with Blue/Green deployment. The application deployed is a simple HTML site.

# Requirements

1) Ubuntu instance on EC2 (can be done locally as well)
2) Jenkins
   - Blue Ocean Plugin
   - Docker Plugin
   - Pipeline:AWS Plugin
3) Docker (requires account)
4) EKS
5) GitHub 
6) Configue Docker, GitHub and AWS credentials in Jenkins


# Steps Performed

1) Run EKS
  - can be done manually or through a script (Following can be in your script)
  
  eksctl create cluster \
--name <cluster_name> \
--version 1.18 \
--nodegroup-name standard-workers \
--node-type t2.micro \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \
--node-ami auto

2) Blue Image:

>./blue/run_docker.sh

>./blue/upload_docker.sh

3) Green Image:

>./green/run_docker.sh 

>./green/upload_docker.sh

4) Run replication controller for Blue Deployment

#kubectl apply -f ./blue-controller.yaml

5) Run replication controller for Green Deployment

#kubectl apply -f ./green-controller.yaml

6) Create the service for the replication

#kubectl apply -f ./website-service.yaml

7) Get load-balancer data

#kubectl get svc

8) DNS for LB should be showing the blue website

9) change service to green deployment

10) DNS for LB should be showing the green website



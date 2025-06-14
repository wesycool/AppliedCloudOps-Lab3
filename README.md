## Overview
Lab 3: The objective is to containerize and deploy a Spring Boot application as a service to a Kubernetes cluster.  Run a vulnerability scan on the container and remediate critical vulnerabilities.  Rebuild and redeploy the application as a rolling upgrade. 

## Lab Report

Your report on this lab will be the basis for your grade.  The purpose of the report is to demonstrate to your instructor that you have completed the lab successfully and understood the material.   

Please include a short paragraph (100 words or less) explaining the difference between the scan output for both branch latest and branch fix.  What is the difference between the two versions and why one scan result is better than the other? 

Please include the following screenshots as part of your evidence. 

- When you have created the service for the first time, include a screenshot of the output from the kubectl get svc command, highlighting the value in the External-IP column that applies to your service.  Also include a screenshot of your web browser to include the address bar for this URL. 

- Ensure you take screenshots that capture the shift from the containers running under one deployment based on one image version, to the transition to a new deployment with new containers using the fix image, e.g., kubectl get svc, kubectl get pods, kubectl get deployment, kubectl describe pod <podname> 

- When you have completed all steps in the lab, take the following screenshots: 

    - Your Docker Hub repo, to include latest and fix image versions. 
    - Scan results from Snyk for both latest and fix images. 

A portion of the grade will be allocated to the quality of the report.  The report should be well formatted, concise and to the point.   


## Instructions

You will need a Kubernetes cluster to complete this lab.  For most of the course we have used Google Kubernetes Engine, so it is probably the best option for this lab, given that most of the material from classes has been created using this platform. 

1. Spin up an EC2 server from Module6_Class3_Repo3_JenkinsForSpringBootDockerBuild repo.  This will be used as a build server as it has docker, maven and java installed.  You will not need to use Jenkins for this lab. 

2. Fork the code in the Module6_Lab3_SpringBootVulnerabilityRemediationOnK8s repo to your own GitHub account. 

3. Create a new developer token in GitHub.  Using your username and this token, clone the forked code to the EC2 build server. 

4. Using branch latest, build the jar file, containerize the application and push to your Docker Hub repo.  From the build machine connect to Docker Hub using the docker login command.  You will be prompted for your username and password.  Use the docker build and push commands to add the image to your repo. 

5. Modify the Module6_Lab3_SpringBootVulnerabilityRemediationOnK8s spring-boot-deployment.yml so that it supports rolling updates.  The approach for rolling upgrades was covered in class 8 of this course; review code and ppt from that class.  Update the image details in the deployment file to match your repo with the latest tag. Deploy the application. Monitor the progress of the Rolling Update through kubectl commands. 

6. Take a screenshot of the output from the kubectl get svc command, highlighting the external IP and a screenshot of your browser showing the application running and including the address bar with the URL/IP address visible. 

7. Create a Snyk account.  You will need to create a token in Docker Hub for your account which you then use in Snyk to connect back to your Docker Hub repo.  Once connected, scan the image that you created using the latest branch.  Review the findings. 

8. On the EC2 build machine, change to the fix branch.  Rebuild the code, containerize the application with the tag fix and push this new image to your Docker Hub repo. 

9. Change the spring-boot-deployment.yml to reference the new image, tagged fix and apply. Ensure you take screenshots that capture the shift from the containers running under one deployment based on one image version to the transition to a new deployment with new containers using the fix image. 

10. Finally take a screenshot of the browser showing the new code running with the external IP of the service visible in the address bar. 
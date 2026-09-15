# Jenkins_practice

This repository contains beginner-friendly Jenkins practice examples and steps. It includes basic freestyle jobs, GitHub webhook automation, both Declarative and Scripted pipeline examples, and a full React + Jenkins + Vercel CI/CD pipeline example.

## Repository Structure
- [My_first_job/](./My_first_job/): Contains the basic manual-trigger Jenkins job notes.
- [Github_onPush/](./Github_onPush/): Contains the GitHub push-triggered Jenkins job notes.
- [Cleanup_job/](./Cleanup_job/): Contains the scheduled cleanup job notes and the sample app build folder.
- [Declarative vs Scripted Pipelines/](./Declarative%20vs%20Scripted%20Pipelines/): Contains notes and examples for both Jenkins pipeline styles.
- [Full_CI_CD_Pipeline/](./Full_CI_CD_Pipeline/): Contains the React app pipeline setup for Jenkins and Vercel deployment.
- [Jenkins_setup_EC2/](./Jenkins_setup_EC2/): Contains the EC2 setup guide for installing Jenkins on an Ubuntu instance with Java 21 and opening port 8080.
- [Jenkins_CICD_EC2/](./Jenkins_CICD_EC2/): Contains the React app deployment pipeline notes for Jenkins running on an EC2 instance.

## Learning Notes
- [My_first_job/my_first_job.md](./My_first_job/my_first_job.md): A very basic first Jenkins job on `http://localhost:8080` that is triggered manually and prints `Hello world from Jenkins` with no extra settings enabled.
- [Github_onPush/github_onPush.md](./Github_onPush/github_onPush.md): A Jenkins job triggered by GitHub pushes to the `main` branch, using a GitHub webhook and an ngrok tunnel to reach local Jenkins.
- [Cleanup_job/cleanup_job.md](./Cleanup_job/cleanup_job.md): A Jenkins job named `cleanup_job` that runs every minute and deletes old `.log` files from the sample app build folder.
- [Declarative vs Scripted Pipelines/declarative_job.md](./Declarative%20vs%20Scripted%20Pipelines/declarative_job.md): A simple Declarative Pipeline example with `Build`, `Test`, and `Deploy` stages.
- [Declarative vs Scripted Pipelines/scripted_job.md](./Declarative%20vs%20Scripted%20Pipelines/scripted_job.md): A Scripted Pipeline example that demonstrates the same stages with Groovy-based syntax.
- [Full_CI_CD_Pipeline/reactjs-pipeline.md](./Full_CI_CD_Pipeline/reactjs-pipeline.md): A full GitHub push-to-deploy flow where GitHub sends a webhook to Jenkins through ngrok, Jenkins runs the repository Jenkinsfile, and the app is deployed to Vercel using a Jenkins credential.
- [Jenkins_setup_EC2/jenkins_setup_ec2.md](./Jenkins_setup_EC2/jenkins_setup_ec2.md): A step-by-step guide to installing Jenkins on an EC2 Ubuntu instance using `openjdk-21-jdk`, enabling the Jenkins service, and opening port `8080` in the EC2 security group.
- [Jenkins_CICD_EC2/reactjs_EC2_pipeline.md](./Jenkins_CICD_EC2/reactjs_EC2_pipeline.md): A Jenkins pipeline that deploys a React app to an EC2 instance, installs dependencies, builds the app, and starts it on port `5173`.

# Jenkins_practice

This repository contains beginner-friendly Jenkins practice examples. It includes basic freestyle jobs, GitHub webhook automation, and both Declarative and Scripted pipeline examples.

## Repository Structure
- [My_first_job/](./My_first_job/): Contains the basic manual-trigger Jenkins job notes.
- [Github_onPush/](./Github_onPush/): Contains the GitHub push-triggered Jenkins job notes.
- [Cleanup_job/](./Cleanup_job/): Contains the scheduled cleanup job notes and the sample app build folder.
- [Declarative vs Scripted Pipelines/](./Declarative%20vs%20Scripted%20Pipelines/): Contains notes and examples for both Jenkins pipeline styles.

## Learning Notes
- [My_first_job/my_first_job.md](./My_first_job/my_first_job.md): A very basic first Jenkins job on `http://localhost:8080` that is triggered manually and prints `Hello world from Jenkins` with no extra settings enabled.
- [Github_onPush/github_onPush.md](./Github_onPush/github_onPush.md): A Jenkins job triggered by GitHub pushes to the `main` branch, using a GitHub webhook and an ngrok tunnel to reach local Jenkins.
- [Cleanup_job/cleanup_job.md](./Cleanup_job/cleanup_job.md): A Jenkins job named `cleanup_job` that runs every minute and deletes old `.log` files from the sample app build folder.
- [Declarative vs Scripted Pipelines/declarative_job.md](./Declarative%20vs%20Scripted%20Pipelines/declarative_job.md): A simple Declarative Pipeline example with `Build`, `Test`, and `Deploy` stages.
- [Declarative vs Scripted Pipelines/scripted_job.md](./Declarative%20vs%20Scripted%20Pipelines/scripted_job.md): A Scripted Pipeline example that demonstrates the same stages with Groovy-based syntax.
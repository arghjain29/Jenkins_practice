# Jenkins_practice

This repository contains beginner-friendly Jenkins practice examples. The latest commit reorganized the files into dedicated folders for each job so the project is easier to browse and maintain.

## Repository Structure
- [`cleanup_job/`](./cleanup_job/): Contains the cleanup job notes and the sample app build folder used by the scheduled log cleanup job.
- [`github_onPush/`](./github_onPush/): Contains the GitHub push-triggered Jenkins job notes.
- [`my_first_job/`](./my_first_job/): Contains the basic manual-trigger Jenkins job notes.

## Learning Notes
- [`cleanup_job/cleanup_job.md`](./cleanup_job/cleanup_job.md): A Jenkins job named `cleanup_job` that runs every minute and deletes old `.log` files from the sample app build folder.
- [`github_onPush/github_onPush.md`](./github_onPush/github_onPush.md): A Jenkins job triggered by GitHub pushes to the `main` branch, using a GitHub webhook and an ngrok tunnel to reach local Jenkins.
- [`my_first_job/my_first_job.md`](./my_first_job/my_first_job.md): A very basic first Jenkins job on `http://localhost:8080` that is triggered manually and prints `Hello world from Jenkins` with no extra settings enabled.
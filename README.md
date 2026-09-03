# Jenkins_practice

This repository is for practicing and learning Jenkins with simple, beginner-friendly examples.

## Learning Notes
- [`my_first_job.md`](./my_first_job.md): A very basic first Jenkins job on `http://localhost:8080` that is triggered manually and prints `Hello world from Jenkins` with no extra settings enabled.
- [`github_onPush.md`](./github_onPush.md): A Jenkins job triggered by GitHub pushes to the `main` branch, using a GitHub webhook and an ngrok tunnel to reach local Jenkins.
- [`cleanup_job.md`](./cleanup_job.md): A Jenkins job named `cleanup_job` that runs every minute and deletes old `.log` files from the sample app build folder.
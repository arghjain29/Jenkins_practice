# ReactJS CI/CD Pipeline with Jenkins on EC2

This project shows how to deploy a React app from GitHub to an EC2 instance using Jenkins. The EC2 and Jenkins installation steps are already explained in the guide named `Jenkins_setup_EC2/jenkins_setup_ec2.md`, so this file focuses only on the CI/CD pipeline setup for the React app.

## Workflow

When code is pushed to the GitHub repository:

1. GitHub sends a webhook request to Jenkins.
2. Jenkins starts the pipeline job.
3. Jenkins checks out the source code.
4. Jenkins installs Node.js dependencies.
5. Jenkins builds the React application.
6. Jenkins copies the project files to the EC2 server.
7. Jenkins starts the preview server on port `5173`.

## Prerequisites

Before continuing, make sure:

- Jenkins is already set up on EC2 using the steps in `Jenkins_setup_EC2/jenkins_setup_ec2.md`.
- Node.js is installed on the EC2 instance.
- Git is installed on the EC2 instance.
- Port `8080` is open for Jenkins.
- Port `5173` is open in the EC2 security group if you want to access the app from the browser.
- The Jenkins user has permission to run the deployment steps, especially if you are using `sudo`.

## Add the GitHub Webhook

1. Open your GitHub repository.
2. Go to **Settings** -> **Webhooks** -> **Add webhook**.
3. Set the **Payload URL** to the public URL of your Jenkins EC2 instance:

```text
http://<EC2_PUBLIC_IP>:8080/github-webhook/
```

4. Set the **Content type** to `application/json`.
5. Select **Just the push event**.
6. Click **Add webhook**.

This means every push to the main branch triggers the Jenkins pipeline automatically.

## Create the Jenkins Pipeline Job

1. Open Jenkins in the browser.
2. Click **New Item**.
3. Enter a job name such as `reactjs-ec2-pipeline`.
4. Select **Pipeline** and click **OK**.
5. In the **Pipeline** section, choose **Pipeline script from SCM**.
6. Set the repository URL to your GitHub project.
7. Select **Git** as the SCM.
8. In **Branches to build**, choose `main`.
9. Set **Script Path** to:

```text
Jenkinsfile
```

10. Click **Save**.

## Jenkinsfile

The Jenkinsfile below checks out the project, installs dependencies, builds the app, and deploys it to `/var/www/react_app` on the EC2 instance.

```groovy
node {
    def appDir = '/var/www/react_app'

    stage('Clean Workspace') {
        echo 'Cleaning workspace...'
        deleteDir()
    }

    stage('Checkout Code') {
        echo 'Checking out code from Git...'
        git (
            branch: 'main',
            url: 'https://github.com/arghjain29/react_ec2_jenkins_pipeline'
        )
    }

    stage('Install Dependencies') {
        echo 'Installing dependencies...'
        sh 'npm install'
    }

    stage('Build Application') {
        echo 'Building React application...'
        sh 'npm run build'
    }

    stage('Deploy Application') {
        echo 'Deploying application to EC2...'
        sh """
        sudo mkdir -p ${appDir}
        sudo chown -R jenkins:jenkins ${appDir}

        rsync -av --delete \
        --exclude='.git' \
        --exclude='node_modules' \
        ./ ${appDir}/

        cd ${appDir}
        sudo npm install
        sudo npm run build
        sudo npm run preview -- --host 0.0.0.0 --port 5173 > /tmp/react_app.log 2>&1 &
        """
    }
}
```

## What This Jenkinsfile Does

- `git` downloads the latest code from GitHub.
- `npm install` installs all project dependencies.
- `npm run build` creates the production build.
- `rsync` copies the project files to the EC2 app folder.
- `npm run preview -- --host 0.0.0.0 --port 5173` starts the preview server in the background on port `5173`.

## Check the Deployment

Once the pipeline finishes successfully, open the browser and visit:

```text
http://<EC2_PUBLIC_IP>:5173
```

If the app loads, the Jenkins deployment is working correctly.

## Security Group Setup

To access the app from the browser, open the EC2 security group and add an inbound rule for port `5173`.

- Type: **Custom TCP**
- Port range: **5173**
- Source: **0.0.0.0/0**

This allows the browser to reach the deployed React app over the internet.

## Result

After the setup is complete:

- A push to GitHub triggers Jenkins automatically.
- Jenkins pulls the repository code.
- Jenkins installs dependencies and builds the app.
- The app is deployed to the EC2 server.
- The app is visible on the EC2 public IP on port `5173`.

You can check the pipeline logs in Jenkins by opening the job and clicking **Console Output** to inspect each stage.

> This setup is useful for learning and testing. For a production deployment, it is better to serve the app using Nginx or a proper web server instead of the Vite preview server.

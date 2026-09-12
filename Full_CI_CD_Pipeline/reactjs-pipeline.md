# ReactJS CI/CD Pipeline with Jenkins and Vercel

This pipeline automates deployment of the React app whenever code is pushed to the GitHub repository. GitHub sends a webhook call to Jenkins through ngrok, Jenkins receives the event, runs the `Jenkinsfile` inside the app, and then deploys the app to Vercel using a token stored in Jenkins credentials.

## Workflow

When a push happens on GitHub:

1. GitHub sends a webhook request to the public Jenkins URL exposed through ngrok.
2. Jenkins receives the webhook event.
3. Jenkins runs the pipeline defined in the project `Jenkinsfile`.
4. The pipeline installs dependencies, builds the app, and deploys it to Vercel.

## Start Jenkins Through ngrok

Jenkins must be reachable from the internet so GitHub can send the webhook call. Keep Jenkins running on `http://localhost:8080`, then open a new terminal and start ngrok.

1. Authenticate ngrok once with your ngrok authtoken:

```bash
ngrok config add-authtoken <your-ngrok-authtoken>
```

2. Forward the Jenkins port:

```bash
ngrok http 8080
```

3. Copy the HTTPS forwarding URL shown by ngrok, for example:

```text
https://example.ngrok-free.app
```

Keep ngrok running while testing. If the ngrok tunnel restarts, the public URL may change, so update your GitHub webhook URL if needed.

## Add the GitHub Webhook

1. Open the GitHub repository.
2. Go to **Settings** -> **Webhooks** -> **Add webhook**.
3. Set the **Payload URL** to your ngrok URL followed by the Jenkins GitHub webhook path:

```text
https://example.ngrok-free.app/github-webhook/
```

4. Set the **Content type** to `application/json`.
5. Select **Just the push event**.
6. Click **Add webhook**.

Now, every push to the repository triggers Jenkins automatically.

## Create the Jenkins Pipeline Job

1. Open Jenkins at `http://localhost:8080`.
2. Click **New Item**.
3. Enter a job name such as `reactjs-pipeline`.
4. Select **Pipeline** and click **OK**.
5. Under **Pipeline**, choose **Pipeline script from SCM**.
6. Set the repository URL to your GitHub project.
7. Select **Git** under **SCM**.
8. In **Branches to build**, use `main`.
9. Set **Script Path** to:

```text
Jenkinsfile
```

10. Click **Save**.

## Jenkinsfile Content

The project contains a Jenkinsfile that installs dependencies, builds the app, and deploys it to Vercel.

```groovy
pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel_token')
    }
    
    stages {
        stage('Install Dependencies'){
            steps {
                echo '[Installing dependencies...]'
                bat 'npm install'
                echo '[Dependencies installed successfully.]'
            }
        }
        stage('Testing Application'){
            steps {
                echo '[Running tests...]'
                echo '[Running unit tests...]'
                echo '[Skipping Tests for now.]'
            }
        }
        stage('Building Application'){
            steps {
                echo '[Building application...]'
                bat 'npm run build'
                echo '[Application built successfully.]'
            }
        }
        stage('Deploy to Vercel'){
            steps {
                echo '[Deploying application to Vercel...]'
                bat 'npx vercel --token %VERCEL_TOKEN% --prod --yes'
                echo '[Application deployed to Vercel successfully.]'
            }
        }
    }
}
```

This means:

- `npm install` installs the project dependencies.
- `npm run build` creates the production build.
- `npx vercel --token %VERCEL_TOKEN% --prod --yes` deploys the built app to Vercel.

## Set Up the Vercel Token

To deploy successfully, Jenkins needs a Vercel token.

### Create a Vercel token

1. Log in to your Vercel dashboard.
2. Go to **Account Settings**.
3. Open the **Tokens** section.
4. Click **Create Token**.
5. Copy the generated token.

### Store the token in Jenkins

1. Open Jenkins.
2. Go to **Manage Jenkins** -> **Credentials**.
3. Click **System** -> **Global credentials** -> **Add Credentials**.
4. Select **Secret text**.
5. In **Secret**, paste the Vercel token.
6. Set the **ID** as:

```text
vercel_token
```

7. Click **OK**.

The Jenkinsfile uses this exact ID in the environment block:

```groovy
environment {
    VERCEL_TOKEN = credentials('vercel_token')
}
```

This allows Jenkins to securely pass the token to the `vercel` deployment command without exposing it in the repository.

## Result

After everything is set up:

- A push to GitHub triggers the webhook.
- GitHub calls Jenkins through ngrok.
- Jenkins runs the `Jenkinsfile` in the project.
- The app is built and deployed to Vercel automatically.

You can check the Jenkins pipeline logs in the **Console Output** to confirm each step runs successfully.

> Never commit your ngrok authtoken or Vercel token to the repository. Store them in Jenkins credentials instead.

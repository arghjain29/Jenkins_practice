# Jenkins Job Triggered by a GitHub Push

This job runs when code is pushed to the `main` branch on GitHub and prints:

`build trigger from Github`

## Start Jenkins Through ngrok

Jenkins must be reachable from the internet so that GitHub can send its webhook. Keep Jenkins running on `http://localhost:8080`, then start ngrok in a terminal.

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

Keep ngrok running while testing. The public URL can change when the ngrok tunnel is restarted.

## Create the Jenkins Job

1. Open Jenkins at `http://localhost:8080`.
2. Click **New Item**.
3. Enter a job name, such as `github-on-push`.
4. Select **Freestyle project** and click **OK**.
5. Under **Source Code Management**, select **Git**.
6. Enter the GitHub repository URL, for example:

```text
https://github.com/<username>/<repository>.git
```

7. In **Branches to build**, specify the `main` branch:

```text
*/main
```

8. Under **Build Triggers**, select **GitHub hook trigger for GITScm polling**.
9. Under **Build Steps**, click **Add build step** -> **Execute shell**.
10. Add this command:

```bash
echo "build trigger from Github"
```

11. Click **Save**.

## Add the GitHub Webhook

1. Open the repository on GitHub.
2. Go to **Settings** -> **Webhooks** -> **Add webhook**.
3. Set **Payload URL** to the ngrok URL followed by the Jenkins GitHub webhook path:

```text
https://example.ngrok-free.app/github-webhook/
```

4. Set **Content type** to `application/json`.
5. Select **Just the push event**.
6. Click **Add webhook**.

Push a change to the `main` branch. Jenkins should start the job automatically. Open the build's **Console Output** and confirm that it contains:

```text
build trigger from Github
```

> Never commit your ngrok authtoken to the repository. Use a Jenkins credential for private GitHub repositories.

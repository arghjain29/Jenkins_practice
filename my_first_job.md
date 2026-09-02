# My First Jenkins Job

This is a very simple Jenkins practice job.

## Goal
Create a basic job that runs only when you click **Build Now** and prints:

`Hello world from Jenkins`

## Steps
1. Open Jenkins dashboard at `http://localhost:8080`.
2. Click **New Item**.
3. Enter job name: `my-first-job`.
4. Select **Freestyle project** and click **OK**.
5. In **Build Triggers**, keep all options unchecked (manual run only).
6. In **Build Steps**, click **Add build step** → **Execute shell**.
7. Add this command:

```bash
echo "Hello world from Jenkins"
```

8. Click **Save**.
9. Open the job and click **Build Now**.
10. Open the build output from **Console Output** and confirm the message appears.

That’s it — no extra settings enabled.

# Cleanup Jenkins Job

This Jenkins job is scheduled to run every minute and removes old build log files from the sample app.

## Goal
Clean up the build logs in:

`D:\Codes\Jenkins_practice\sample_app\builds`

and print progress messages in the Jenkins console output.

## Steps
1. Open Jenkins dashboard at `http://localhost:8080`.
2. Click **New Item**.
3. Enter job name: `cleanup_job`.
4. Select **Freestyle project** and click **OK**.
5. In **Build Triggers**, select **Build periodically**.
6. Add the cron schedule:

```text
* * * * *
```

This means the job runs every minute.

7. In **Build Steps**, click **Add build step** → **Execute Windows batch command**.
8. Add these commands:

```batch
echo Cleaning up build Folder

del /q D:\Codes\Jenkins_practice\sample_app\builds\*.log

echo Cleanup Completed
```

9. Click **Save**.
10. Either wait for the scheduled run or click **Build Now** to test it immediately.
11. Open the build output in **Console Output** and confirm that the job prints:

```text
Cleaning up build Folder
Cleanup Completed
```

This keeps the build folder clean by deleting old `.log` files automatically.

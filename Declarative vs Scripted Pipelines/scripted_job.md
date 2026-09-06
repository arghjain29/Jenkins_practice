# Scripted Jenkins Pipeline

This job is created as a Jenkins pipeline project using the Scripted Pipeline syntax. Scripted pipelines are based on Groovy and give you more flexibility, but they are usually less structured than declarative pipelines.

## Goal
Create a simple scripted pipeline that runs three stages in order: `Build`, `Test`, and `Deploy`. Each stage prints a message in the Jenkins console output so you can see the execution flow.

## Steps
1. Open Jenkins dashboard at `http://localhost:8080`.
2. Click **New Item**.
3. Enter a name such as `scripted-job`.
4. Select **Pipeline** as the item type and click **OK**.
5. In the pipeline configuration page, scroll down to the **Pipeline** section.
6. Choose **Pipeline script** and paste the following code:

```groovy
node {
    stage("Build") {
        echo "Building the Project........."
    }
    stage("Test") {
        echo "Testing the Project........."
    }
    stage("Deploy") {
        echo "Deploying the App........."
    }
}
```

7. Click **Save**.
8. Click **Build Now** to run the pipeline.
9. Open the **Console Output** and check the stage messages:

```text
Building the Project.........
Testing the Project.........
Deploying the App.........
```

## What this pipeline does
- Runs three stages: `Build`, `Test`, and `Deploy`
- Uses the `node` block to allocate an executor for the pipeline run
- Prints a message in each stage to track progress
- Demonstrates the Scripted Pipeline style, which is more flexible and Groovy-based compared to Declarative syntax

# Declarative Jenkins Pipeline

This job is created as a Jenkins pipeline project using the Declarative Pipeline syntax. Declarative pipelines are easier to read and maintain because the structure is clearly defined with stages and steps.

## Goal
Create a simple pipeline job that runs three stages in order: `Build`, `Test`, and `Deploy`. Each stage prints a message to the Jenkins console output so you can see the flow of execution.

## Steps
1. Open Jenkins dashboard at `http://localhost:8080`.
2. Click **New Item**.
3. Enter a name such as `declarative-job`.
4. Select **Pipeline** as the item type and click **OK**.
5. In the pipeline configuration page, scroll down to the **Pipeline** section.
6. Choose **Pipeline script** and paste the following code:

```groovy
pipeline {
    agent any
    
    stages {
        stage ("Build") {
            steps {
                echo "Building the Project......."
            }
        }
        stage ("Test") {
            steps {
                echo "Testing the Project......."
            }
        }
        stage ("Deploy") {
            steps {
                echo "Deploying the App......."
            }
        }
    }
}
```

7. Click **Save**.
8. Click **Build Now** to run the pipeline.
9. Open the **Console Output** and check the stage messages:

```text
Building the Project.......
Testing the Project.......
Deploying the App.......
```

## What this pipeline does
- Runs three stages: `Build`, `Test`, and `Deploy`
- Uses the `agent any` directive so Jenkins can run it on any available agent
- Prints a message in each stage to show execution progress
- Demonstrates the Declarative Pipeline structure, which is commonly used in real Jenkins CI/CD workflows

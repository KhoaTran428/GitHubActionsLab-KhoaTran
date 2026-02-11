Dependent Jobs Workflow (CI/CD Pipeline)
This repository demonstrates a sequential execution pipeline using GitHub Actions. Unlike parallel jobs, this workflow ensures that each stage of the software lifecycle only begins if the previous stage completes successfully.

The dependent-jobs.yml workflow simulates a standard software release cycle through three distinct stages:

Build: Compiles the source code and prepares artifacts.

Test: Validates the integrity of the build.

Deploy: Pushes the validated build to a production or staging environment.

Key Concepts Demonstrated
Job Dependencies (needs)
The core of this workflow is the needs keyword. It creates a linear requirement chain:

The Test job will stay in a "Queued" state until the Build job finishes.

The Deploy job will only trigger if the Test job returns a success exit code.

Note: If any job in the chain fails, all subsequent jobs are automatically skipped. This prevents broken code from ever reaching the deployment phase.

Challenges & Resolutions
Challenge: If the "Build" job fails, the "Deploy" job shouldn't run, but sometimes you still want "Cleanup" tasks to occur.

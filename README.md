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


Multi-OS GitHub Actions Workflow
This repository demonstrates a cross-platform CI/CD pipeline using GitHub Actions. The workflow is designed to validate code execution across the three primary operating systems supported by GitHub-hosted runners: Linux (Ubuntu), Windows, and macOS.

Purpose of the Workflow
The primary goal of this workflow is to ensure environment parity. By running independent jobs on different operating systems, we can:

Verify Compatibility: Ensure scripts and build processes work across different kernels and shells.

Parallel Testing: Execute tasks simultaneously to reduce the total "Time to Feedback" for developers.

OS-Specific Validation: Run commands unique to each system (e.g., systeminfo vs. uname) to confirm the runner environment.

Key Concepts Demonstrated
runs-on
This attribute defines the virtual machine image used for the job.

ubuntu-latest: A standard Linux environment (currently Ubuntu 22.04 or 24.04).

windows-latest: A Windows Server environment (currently Windows Server 2022).

macos-latest: A macOS environment (currently running on Apple Silicon/M1).

needs (Concurrency vs. Dependency)
In this specific workflow, the needs keyword is omitted.

Without needs: Jobs run in parallel. ubuntu-job, windows-job, and macos-job start at the same time.

With needs: You can create a sequential chain (e.g., "Deploy" only after "Test" passes).

Challenges & Resolutions
Line Endings (CRLF vs. LF)
Challenge: When creating files across different OSs, line endings can cause checksum failures or script errors.

Resolution: By using the standard echo command within the runner's native shell, the runner handles the appropriate line ending for that specific environment automatically.




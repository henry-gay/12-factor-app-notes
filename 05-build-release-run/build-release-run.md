# 05 - Build, Release, Run

## Summary
The **Build, Release, Run** factor of the 12-Factor App methodology emphasizes a clear distinction between the stages of deployment. The application must follow a strict separation of the build, release, and run stages in its lifecycle.

## Key Principles
1. **Strict Separation of Build, Release, and Run**
    - **Build**: This stage is responsible for creating a deployable artifact (e.g., compiling code, packaging the application).
    - **Release**: The release stage includes combining the build artifact with configuration values and storing the release for deployment.
    - **Run**: This stage runs the application in a particular environment (e.g., starting the web server or application process).

2. **Immutable Releases**
    - Once a release is created, it must be immutable. This ensures that the same release can be deployed multiple times without changes.

3. **Clear Stage Transitions**
    - Each stage (build, release, run) should be fully automated and transparent, with clear separation between them.

## Best Practices
- Use a **CI/CD pipeline** to automate the build, release, and run process.
- Store the build artifacts in versioned containers (e.g., Docker images) or similar.
- Ensure all environment-specific configuration is injected at the release stage, not during build or run.
- Implement a clear and repeatable process to promote builds from one environment to another (e.g., dev to staging to production).

## Example
### Build, Release, Run Process
1. **Build**: Compile code, package it, create an artifact (e.g., Docker image).
2. **Release**: Apply configuration to the artifact, storing it as a release version.
3. **Run**: Deploy the release to the desired environment, running it as a process (e.g., web server).

### Example: Using Docker for Build, Release, and Run
**Build Stage:**
```
# Build the Docker image
docker build -t my-app .
```
**Release Stage:**
```
# Release the Docker image with configuration
docker run -d -e DATABASE_URL=postgres://localhost/mydb my-app
```
**Run Stage:**
```
# Running the Docker container
docker start my-app
```

## Additional Resources
- [12factor.net - Build, Release, Run](https://12factor.net/build-release-run)
- [CI/CD with GitLab](https://docs.gitlab.com/ee/ci/)
- [Docker Documentation](https://docs.docker.com/)
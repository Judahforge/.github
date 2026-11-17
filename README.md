# Node.js CI/CD Pipeline with GitHub Actions & Docker

## Overview

This project implements an automated CI/CD workflow using **GitHub Actions** to build, test, and containerize a Node.js application.

The workflow is triggered whenever code is pushed to the `main` branch or when a pull request is opened against `main`. It automates dependency installation, application building, testing, and Docker image publishing to Docker Hub.

The goal is to establish a consistent and repeatable integration pipeline that helps maintain application quality and simplifies container image delivery.

## Workflow Architecture

The pipeline follows these stages:

1. **Code Checkout:** Retrieves the latest source code from the GitHub repository.
2. **Node.js Setup:** Configures the Node.js environment and enables npm dependency caching.
3. **Dependency Installation:** Installs project dependencies using `npm ci` for a clean and consistent installation.
4. **Application Build:** Executes the build script defined in `package.json`.
5. **Automated Testing:** Runs the project's test suite using `npm test`.
6. **Docker Image Build & Push:** Builds a Docker image and publishes it to Docker Hub.
7. **Debugging:** Displays the configured Docker Hub username and the installed Node.js version.

## Technologies Used

- **GitHub Actions** – Workflow automation and CI/CD orchestration.
- **Node.js** – JavaScript runtime environment.
- **NPM** – Package and dependency management.
- **Docker** – Application containerization.
- **Docker Hub** – Container image registry.
- **Ubuntu Latest** – GitHub-hosted runner environment.

## Workflow Triggers

The workflow runs automatically on:

| Event | Target Branch |
|---|---|
| Push | `main` |
| Pull Request | `main` |

## Prerequisites

Before running the workflow, ensure that:

- The repository contains a valid Node.js application.
- A `package.json` file is available in the project root.
- The project defines the `build` and `test` scripts.
- A valid `Dockerfile` exists in the repository root.
- A Docker Hub account is available.

## GitHub Repository Secrets

The workflow requires the following repository secrets to authenticate with Docker Hub:

| Secret | Description |
|---|---|
| `DOCKER_USERNAME` | Docker Hub username. |
| `DOCKER_PASSWORD` | Docker Hub access token or password. |

**Configuration:**

Navigate to:

`GitHub Repository → Settings → Secrets and variables → Actions → New repository secret`

Add both secrets using the exact names specified above.

Never hardcode Docker Hub credentials in the workflow file.

## Docker Image

After a successful build and test process, the workflow builds and publishes the Docker image to Docker Hub.

**Image repository:**

`blakiowrld/my-nodejs-app`

**Image tag:**

`latest`

The image can be pulled using:

```bash
docker pull blakiowrld/my-nodejs-app:latest
```

## Running the Workflow

1. Push your code changes to the `main` branch.
2. GitHub Actions automatically detects the push event.
3. The workflow checks out the repository and prepares the Node.js environment.
4. Dependencies are installed, the application is built, and tests are executed.
5. The Docker image is built and published to Docker Hub.
6. Workflow execution results can be monitored under the repository's **Actions** tab.

## Expected Outcome

A successful workflow execution confirms that:

- The repository source code was checked out successfully.
- Node.js dependencies were installed.
- The application build completed successfully.
- Automated tests passed.
- The Docker image was built and published to Docker Hub.

## Conclusion

This project demonstrates the implementation of an automated Node.js CI/CD workflow using GitHub Actions and Docker.

By integrating dependency management, application builds, automated testing, and container image publishing into a single workflow, the pipeline provides a repeatable approach to software integration and container delivery.

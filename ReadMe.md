# Trivy Scan on Windows with HTML Report

This guide walks you through scanning an existing Docker image using Trivy on a Windows PC and generating an HTML report.

## Prerequisites

- Docker Desktop installed and running on your Windows PC.
- A local Docker image available for scanning (e.g., `python:3.4-alpine`).

## Steps

1. **Run the Trivy Scan:**

    Use the following command to run the Trivy scan on your local Docker image and generate an HTML report.

    ```sh
    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v C:\ESD:/output aquasec/trivy image --template "@/output/template.html" -f template -o /output/trivy-report.html python:3.4-alpine
    ```

    Explanation:
    - `--rm`: Automatically removes the container after the command completes.
    - `-v /var/run/docker.sock:/var/run/docker.sock`: Mounts the Docker socket to allow Trivy to communicate with the Docker daemon on the host.
    - `-v C:\ESD:/output`: Mounts your local directory (`C:\ESD`) to the container's `/output` directory. Replace `C:\ESD` with your desired path.
    - `--template "@/output/template.html"`: Specifies the path to the HTML template file inside the container.
    - `-f template`: Specifies the format as `template`.
    - `-o /output/trivy-report.html`: Specifies the output file for the report.
    - `python:3.4-alpine`: Specifies the Docker image to be scanned.

2. **Create an HTML Template:**

    Create a simple HTML template file (e.g., `template.html`) and save it in your desired location (e.g., `C:\ESD\template.html`).

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Trivy Scan Report</title>
    </head>
    <body>
        <h1>Trivy Scan Report</h1>
        <pre>{{ . }}</pre>
    </body>
    </html>
    ```

3. **Run the Scan Command:**

    Execute the command provided in step 1. Ensure that the specified directory (`C:\ESD`) exists or create it beforehand.

    This command will generate an HTML report of the scan and save it as `trivy-report.html` in the specified directory on your Windows PC.

## Example

Here is an example command using PowerShell, assuming you want to save the output in `C:\ESD`:

```sh
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v C:\ESD:/output aquasec/trivy image --template "@/output/template.html" -f template -o /output/trivy-report.html python:3.4-alpine
```
# Jenkins Node.js Pipeline

This repository contains a simple Jenkins declarative pipeline that runs inside a Docker container with Node.js 16.

## Overview

The pipeline is designed to:
1. Run in a Docker container using the `node:16-alpine` image.
2. Check the Node.js installation by printing the version.


Prerequisites
To run this pipeline, you need:

A Jenkins instance with Docker installed and configured.
The Docker Pipeline plugin installed on Jenkins.
How It Works
Docker Agent: The pipeline runs inside a Docker container using the lightweight Node.js image node:16-alpine.

Test Stage:

Executes the command node --version to verify the Node.js environment is set up correctly.
How to Use
Clone this repository:


git clone <repository-URL>
cd <repository-name>
Add the Jenkinsfile to a Jenkins pipeline project.

Run the pipeline on your Jenkins server.

View the console output to confirm the Node.js version is displayed.

Example Output
If the pipeline runs successfully, you’ll see output like this in Jenkins:


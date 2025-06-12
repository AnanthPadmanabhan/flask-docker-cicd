# Flask Docker CI/CD Example

This is a simple Flask application with a Dockerfile and Jenkinsfile for implementing CI/CD using Docker Desktop and Jenkins.

## 🚀 Run Locally

```bash
docker build -t flask-docker-cicd .
docker run -p 5000:5000 flask-docker-cicd
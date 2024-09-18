# Flask-or-FastAPI-application-on-Azure-Web-App


![image](https://github.com/user-attachments/assets/b62a9b4e-e5bc-4056-aebe-c40df30023b7)

This repository contains a simple Flask/FastAPI web application deployed on Azure Web Apps with CI/CD integration using GitHub Actions.

Application Overview
This app demonstrates how to deploy a basic Flask or FastAPI application to Azure Web Apps. The app has a single endpoint (/) that returns:

## Hello, Azure Web Apps!

# Deploying to Azure Web Apps
a. Create an Azure Web App
Log in to the Azure Portal.
Navigate to App Services and create a new Web App.
Choose Python 3.x as the runtime stack.
Select Linux as the OS.
b. Configure Deployment from GitHub
In the Azure Web App menu, navigate to Deployment Center.
Choose GitHub as the deployment source and select your repository.
4. CI/CD Setup with GitHub Actions
This repository includes a GitHub Actions workflow to automatically deploy the app to Azure Web Apps on every push to the main branch.

GitHub Actions Workflow (located in .github/workflows/azure-webapps.yml):

c. Configure Azure Publish Profile
Download the Azure Web App's publish profile from the Azure Portal.
Add the publish profile as a GitHub secret:
Go to your repository settings.
Add a new secret named AZURE_WEBAPP_PUBLISH_PROFILE.

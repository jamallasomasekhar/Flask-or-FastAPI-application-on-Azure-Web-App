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
## 4. CI/CD Setup with GitHub Actions
This repository includes a GitHub Actions workflow to automatically deploy the app to Azure Web Apps on every push to the main branch.

### GitHub Actions Workflow (located in .github/workflows/azure-webapps.yml):
name: Build and deploy Python app to Azure Web App - flaskapp

on:
  push:
    branches:
      - master
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python version
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      - name: Create and start virtual environment
        run: |
          python -m venv venv
          source venv/bin/activate
      
      - name: Install dependencies
        run: pip install -r requirements.txt
        
      # Optional: Add step to run tests here (PyTest, Django test suites, etc.)

      - name: Zip artifact for deployment
        run: zip release.zip ./* -r

      - name: Upload artifact for deployment jobs
        uses: actions/upload-artifact@v4
        with:
          name: python-app
          path: |
            release.zip
            !venv/
  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'Production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}
    
    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v4
        with:
          name: python-app

      - name: Unzip artifact for deployment
        run: unzip release.zip

      
      - name: 'Deploy to Azure Web App'
        uses: azure/webapps-deploy@v3
        id: deploy-to-webapp
        with:
          app-name: 'flaskapp'
          slot-name: 'Production'
          publish-profile: ${{ secrets.AZUREAPPSERVICE_PUBLISHPROFILE_5861604C7CE9481BBF70F15C6EB8087B }}

c. Configure Azure Publish Profile
Download the Azure Web App's publish profile from the Azure Portal.
Add the publish profile as a GitHub secret:
Go to your repository settings.
Add a new secret named AZURE_WEBAPP_PUBLISH_PROFILE.
![image](https://github.com/user-attachments/assets/60da73b3-63e7-4ffd-b846-23aa0aaa838b)

![image](https://github.com/user-attachments/assets/66f34c66-a788-4bbb-9504-b669c81c51ec)


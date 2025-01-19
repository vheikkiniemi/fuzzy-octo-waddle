> **NOTE!** The material has been created with the help of the ChatGPT AI application

# HTML, CSS, and JavaScript - PaaS Model

## Introduction to the PaaS Model
- Definition: `Platform as a Service (PaaS)` offers developers a platform to develop, deploy, and manage applications without the need to manage infrastructure.
- Key Features:
    - Infrastructure (servers, networks, storage) is abstracted from the developer.
    - Support for multiple programming languages and frameworks.
    - Built-in scaling, security, and CI/CD support.
- Examples of PaaS Services:
    - Microsoft: `Azure App Service`, `Azure Static Web Apps`, `Azure Functions`.
    - Amazon Web Services (AWS): `AWS Elastic Beanstalk`, `AWS Lambda`.
    - Google Cloud: `Google App Engine`, `Cloud Functions`.
    - Heroku: Application development and deployment.

## Web Application Design with the PaaS Model
- Steps in planning:
    1. Application Requirements:
        - Choose programming languages and technologies.
        - Define necessary features and database requirements.
    2. Choose a Suitable PaaS Platform:
        - Static applications: `Azure Static Web Apps`, `AWS Amplify`, `Google Firebase Hosting`.
        - Dynamic applications: `Azure App Service`, `Google App Engine`, `Heroku`.
    3. Security:
        - Utilize built-in HTTPS and authentication solutions provided by PaaS services (e.g., `Azure Active Directory`, `AWS Cognito`, `Firebase Authentication`).

- **Benefit:** Developers can focus on application functionality instead of infrastructure management.

## Application Development and CI/CD Process
- Development Phase:
    - Write code and test locally (e.g., using Visual Studio Code).
    - Leverage PaaS platform features, such as support for environment variables.
- CI/CD Pipeline:
    - Version control: GitHub, GitLab, Bitbucket.
    - Automate the deployment process:
        - Azure Static Web Apps: Built-in GitHub Actions integration.
        - AWS Elastic Beanstalk: Pipeline support with AWS CodePipeline.
        - Google App Engine: Integrate with Cloud Build pipeline.
        - Heroku: Git-push-based deployment.

- **Benefit**: Updates are deployed automatically, speeding up the development cycle.

## Deploying an Application on a PaaS Platform
- Deployment Steps:
    1. Create a PaaS resource (e.g., Azure Static Web App, AWS Amplify, or Google Firebase Hosting).
    2. Configure application settings, such as domains, environment variables, and security settings.
    3. Deploy the application using tools like GitHub Actions or AWS CodePipeline.

- Example:
    - Deploy an HTML/CSS/JS site to Azure Static Web Apps at: `https://mywebapp.staticweb.app`.
    - Alternatively, use AWS Amplify or Firebase Hosting.
- **Benefit**: A scalable, ready-to-use platform for hosting.

## Maintenance and Optimization
- Application Monitoring:
    - Use `Azure Monitor`, `AWS CloudWatch`, and `Google Cloud Monitoring` to analyze performance and user data.
- Scalability:
    - Platforms like `Azure App Service`, `AWS Elastic Beanstalk`, and `Google App Engine` support automatic scaling based on user demand.
- Cost Optimization:
    - Use appropriate service level plans (e.g., Free, Basic, Premium).
- Security:
    - Keep the application and dependencies up to date.
    - Integrate a custom domain and SSL.

# Case Study: Azure Static Web Apps

> Azure Static Web Apps is an excellent example of the Platform as a Service (PaaS) model. PaaS provides developers with a platform solution where they can focus on the application’s code and functionality without needing to worry about infrastructure maintenance, such as servers, network configurations, or load management.

## Why is Azure Static Web Apps a PaaS?
1. Automated server management:
    - No need to set up servers, install software, or configure environments. Azure handles all hosting-related tasks.
2. Built-in CI/CD support:
    - Direct integration with GitHub or Azure DevOps ensures that code changes are automatically published, a typical feature of PaaS.
3. User-friendly resource management:
    - Scaling, performance optimization, and security (HTTPS) are handled without manual configuration.
4. Support for modern web applications:
    - Hosts static files (HTML, CSS, JavaScript) and supports dynamic features, such as API connections (Azure Functions).

## Azure Static Web Apps vs. Other Cloud Service Models
1. Infrastructure as a Service (IaaS):
    - With IaaS models like Azure Virtual Machines, you must set up and manage your own servers, which is more complex.
    - Static Web Apps simplifies this by eliminating the need for server-level management.
2. Software as a Service (SaaS):
    - SaaS provides ready-to-use software solutions (e.g., Office 365) without requiring development.
    - Static Web Apps is not SaaS because it is a platform for developing and hosting your own applications.
3. Platform as a Service (PaaS):
    - PaaS allows application development, deployment, and management without infrastructure management.
    - Azure Static Web Apps is a PaaS model because it offers a complete environment for hosting and deploying code with automated processes.

## Summary of Azure Static Web Apps
- Azure Static Web Apps is part of the PaaS model because:
    - It automatically manages the infrastructure.
    - It provides a developer-friendly and fast way to publish applications.
    - It supports built-in features such as CI/CD, HTTPS, and API connections without any additional configuration.

## Steps for Deploying a Website Using Azure Static Web Apps

> Check this out: https://learn.microsoft.com/en-us/azure/app-service/

> **Prompt (ChatGPT):** Please tell me the steps required to deploy a website to Azure Static Web Apps. I have an existing html file.

> **Answer:** Here are the steps to deploy your HTML website to Azure Static Web Apps. The process is easy and straightforward.

### 1. Create an Azure Account:
- Go to the [Azure portal](https://azure.microsoft.com/) and create a free account if you don’t already have one.
- `Note: Students at Centria may already have an account provided.`

### 2. Prepare Your HTML Website:
1. Ensure all files are in one folder:
```
/project
├── index.html
├── styles.css (optional)
└── script.js (optional)
```
2. Confirm that index.html is the home page.

### 3. Install the Azure Static Web Apps Extension in VS Code:
1. Open Visual Studio Code.
2. Install the Azure Static Web Apps extension.`Note! The lectures use the Azure App Service extension`:
    - Open the extension manager (Ctrl+Shift+X).
    - Search for Azure Static Web Apps and install it.

### 4. Create a New Azure Static Web App:
1. Sign in to your Azure account in Visual Studio Code.
2. Open the Azure Static Web Apps view and click + (Create new Static Web App).
3. Follow the instructions:
    - Name the app (e.g., MyStaticSite).
    - Select a resource group or create a new one.
    - Choose the Free Plan for testing.
    - Specify the folder containing your HTML files as the publishing source.

### 5. Publish the HTML Site:
1. Choose the project folder containing your HTML files.
2. Azure Static Web Apps automatically sets up a CI/CD pipeline (if using GitHub `Note! We use GitHub by default`). If not: 
    - Azure directly copies and deploys your files.

### 6. Test and Verify:
1. Open the provided link (e.g., `https://polished-mountain-12345.azurestaticapps.net`) in a browser.
2. Verify that all files and styles are working correctly.

### 7. Optional Additional Settings:
1. Custom domain:
    - Add a custom domain (e.g., `www.yourdomain.com`) in the Azure portal.
2. HTTPS:
    - Azure Static Web Apps provides automatic HTTPS protection.
3. API Integration:
    - Add dynamic features using Azure Functions.

### 8. Making Updates:
1. If you modify your HTML files:
    - Open the project in Visual Studio Code.
    - Click Deploy to Static Web App again.
2. Updates will be reflected automatically.

### Summary
- Azure Static Web Apps is perfect for hosting HTML websites without complex infrastructure management.
- It enables fast deployment and provides a scalable and secure environment.
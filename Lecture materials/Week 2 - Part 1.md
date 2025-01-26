> **NOTE!** The material has been created with the help of the ChatGPT AI application

# Static and Dynamic Websites

The differences between a static and dynamic website, client-side and server-side, are based on the way they process and deliver content to users. Here's a comparison.

## Client-Side

### Static Website:
- **Content:** The content is pre-defined and fixed. The same HTML, CSS, and JavaScript are delivered to all users without changes.
- **Interactivity:** Limited. Interactions (e.g., animations or user-triggered content changes) are implemented only via JavaScript, without server support.
- **Loading Speed:** Static websites load faster because the content does not require additional processing on the server.
- **Example:** Simple portfolio or company pages where the content does not change based on user actions.

### Dynamic Website:
- **Content:** The content can change based on user actions, time, or other variables. The frontend may fetch data from the server using technologies like **AJAX** (REST API, GraphQL).
- **Interactivity:** Highly interactive. Content can update dynamically without reloading the entire page.
- **Example:** E-commerce websites where product listings and prices are fetched from the server, or applications like social media platforms.

## Server-Side

### Static Website:
- **Content Generation:** Pages are pre-created as files (HTML, CSS, JavaScript) and simply served to the client by the server.
- **Server Role:** Minimal. The server only acts as a file server (e.g., Nginx or Azure Static Web Apps). No computation or logic is performed.
- **Database:** Usually not used because the content is static and does not need to be fetched or modified.
- **Scalability:** Highly scalable because the server only needs to deliver static files.
- **Example:** GitHub Pages where all content is directly stored as static files.

### Dynamic Website:
- **Content Generation:** Pages are dynamically created or modified on the server based on user requests. For example:
  - A backend application (Node.js, Python, PHP) retrieves data from a database and generates HTML "on the fly."
  - APIs return data that the frontend uses to update the page.
- **Server Role:** Handles user requests, performs computations, fetches data from databases, and may modify content before sending it to the client.
- **Database:** Used for storing and retrieving data (e.g., user details, product lists).
- **Scalability:** Requires more resources because each request may involve computation and database queries. Scalability depends on server performance and optimization.
- **Example:** WordPress websites, e-commerce platforms, applications like Netflix.

## Summary of Differences

| Feature                    | Static Website                            | Dynamic Website                              |
|----------------------------|-------------------------------------------|---------------------------------------------|
| **Content**                | Same for all users                       | Changes based on user actions or data       |
| **Server Role**            | File serving                             | Computation, database querying              |
| **Database**               | Not needed                               | Used (e.g., MySQL, MongoDB)                 |
| **Interactivity**          | Limited                                  | High                                        |
| **Loading Speed**          | Faster                                   | Slower but more advanced                    |
| **Scalability**            | Highly scalable                          | Heavier, requires optimization              |
| **Use Cases**              | Blogs, static company pages              | E-commerce, applications, interactive services |


# PaaS model - One implementation method for the server side

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
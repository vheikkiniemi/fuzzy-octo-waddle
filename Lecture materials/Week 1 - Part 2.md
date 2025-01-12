> **NOTE!** The material has been created with the help of the ChatGPT AI application

# HTML, CSS, and JavaScript - On-Premise and Cloud VM

## Introduction to the HTTP Protocol

### HTTP
- HTTP (HyperText Transfer Protocol) is an application-layer protocol used for transferring data in web applications.
- Specifically developed for use with the World Wide Web (WWW).
- Stateless: Each request is independent of others.

### Basic Principles of HTTP
- **Client–Server Model**:
  - The client makes a request.
  - The server responds accordingly.
- A text-based protocol designed to be human-readable.

### Structure of an HTTP Request
1. **Request Line**:
    - Example: `GET /index.html HTTP/1.1`
2. **Header Fields**:
    - Metadata, e.g., `Host: www.example.com`
3. **Body (optional)**:
    - Contains data for POST or PUT requests.

### Structure of an HTTP Response
1. **Response Line**:
    - Example: `HTTP/1.1 200 OK`
2. **Header Fields**:
    - Example: `Content-Type: text/html`
3. **Body**:
    - The actual content, such as HTML code.

### HTTP Methods
- **GET**: Retrieves data.
- **POST**: Sends data to the server.
- **PUT**: Updates or creates a resource.
- **DELETE**: Deletes a resource.
- **HEAD**: Retrieves only the headers.

### HTTP Status Codes
- **1xx**: Informational responses.
- **2xx**: Successful responses (e.g., `200 OK`).
- **3xx**: Redirections (e.g., `301 Moved Permanently`).
- **4xx**: Client errors (e.g., `404 Not Found`).
- **5xx**: Server errors (e.g., `500 Internal Server Error`).

### HTTP/1.1 and HTTP/2
- **HTTP/1.1**:
  - Supports persistent connections.
  - Improves efficiency with caching and compression.
- **HTTP/2**:
  - Uses a binary format.
  - Multiplexing (multiple requests over a single connection).
  - Better performance.

### HTTP/3 – The Latest Generation
- **HTTP/3** uses the QUIC protocol instead of TCP.
  - QUIC is a UDP-based protocol offering faster and more stable connections.
- Improvements over HTTP/2:
  - **Faster connection establishment**: No three-way handshake like TCP.
  - **Better performance on mobile networks**: Connections remain stable during network changes.
  - **No Head-of-Line Blocking**: Delays caused by a single error do not affect the entire connection.
- **Security**:
  - QUIC includes built-in TLS 1.3 encryption.
- **Use Cases**:
  - Speeds up web applications and services, such as video streaming and real-time applications.
- **Support**:
  - Gaining adoption in browsers (e.g., Chrome, Edge) and servers (e.g., Cloudflare, Google).

### HTTPS – Secure HTTP
- HTTPS uses TLS (Transport Layer Security) encryption.
- Provides:
  - Data encryption.
  - Authentication.
  - Integrity verification.
- Essential for security-critical applications (e.g., banking, e-commerce).
- Now used by nearly every website.

### The Role of HTTP in Modern Web Applications
- Works alongside REST and GraphQL APIs.
- Servers can leverage caching and CDN networks to improve performance.
- HTTP/3 is becoming increasingly common for future applications.

# Introduction to Web Service

## What is a Web Service?
- A service that provides websites or applications to users over the network.
- Typically uses HTTP/HTTPS protocols for communication.

### Goals
- Deliver dynamic or static content to clients (e.g., browsers, mobile apps).
- Key components:
  1. Client (User)
  2. Server
  3. Data transfer via protocol (TCP/UDP, usually port 80 or 443)

## Basic Architecture

### Client–Server Model
- **Client** (e.g., browser or mobile app) sends requests to the server:
  - Uses a specific protocol and port.
  - Typically located in different physical locations → Introduces latency in data transfer.
- **Server** processes the request and returns a response:
  - Processing consumes resources → Adds latency.
  - Delivering the response also introduces delay.

### Components
1. **Web Server**: Handles HTTP requests (e.g., Nginx, Apache).
2. **Application Logic**: Implemented using programming languages (e.g., Node.js, Deno, Python).
3. **Database**: Stores and retrieves data (e.g., PostgreSQL, MongoDB).

## Web Service Development Stages

### 1. Design
- Define the service's goals and features.
- Select technologies (e.g., backend/frontend frameworks and databases).

### 2. Implementation
- Create a server to handle requests.
- Design and code frontend and backend logic.
- Develop API interfaces (REST/GraphQL).

### 3. Testing
- Test functionality, security, and performance.

### 4. Deployment
- Host the service on a web server or in the cloud (e.g., AWS, Azure, Vercel).

## Tools and Technologies

### Frontend Technologies
- **Core**: HTML, CSS, JavaScript.
- **Frameworks**: React, Angular, Vue.js.

### Backend Technologies
- **Core**: Node.js, Deno, Python (Django/Flask), Ruby on Rails.

### Databases
- **Relational**: PostgreSQL, MySQL.
- **NoSQL**: MongoDB, Redis.

### API Interfaces
- REST, GraphQL.

### Hosting
- Cloud platforms: AWS, Google Cloud, Azure.
- Services like Heroku or Vercel.

## Key Considerations

### Security
1. Use HTTPS.
2. Protect input data (e.g., prevent SQL injections).
3. Implement user authentication (e.g., OAuth).

### Scalability
1. Design the service to scale with the user base.
2. Use load balancers and caching.

### Maintenance
1. Keep the server and libraries up to date.
2. Monitor logs and performance.

---

# On-Premise VM and Web Service Deployment

## Introduction to Web Service Deployment on a Virtual Machine

### What is a Virtual Machine (VM)?
- A virtual environment that behaves like a physical computer.
- Hosted using virtualization software (e.g., VirtualBox, VMware, Hyper-V).

### Why Use a Virtual Machine?
- Isolated development environment.
- Easy to manage and replicate.
- Can simulate different operating systems and server environments.
- Cost-effective → No usage-based fees (unlike cloud).
- Ideal for various tests (functionality, performance, security).
- Located nearby physically → Minimal data transfer delays.
- Essential for security testing in a controlled environment.

### Goals
- Deploy a web service on a local VM to simulate a real server environment.

## Steps to Set Up and Prepare a Virtual Machine

1. **Create the VM**:
   - Select virtualization software (e.g., VirtualBox).
   - Install an operating system (e.g., Ubuntu Server).

2. **Configure the VM**:
   - Allocate sufficient resources (RAM, CPU, storage).
   - Configure network settings (NAT, bridged mode).

3. **Install Basic Software**:
   - Web server (e.g., Nginx, Apache).
   - Application runtime (e.g., Node.js, Python).
   - Database (e.g., PostgreSQL, MySQL).

---

## Cloud and Web Service Deployment

### Types of Cloud Service Models

1. **IaaS** (Infrastructure as a Service)
   - **Level**: Infrastructure.
   - **User responsibility**: OS, applications, security.
   - **Provider responsibility**: VMs, storage, networks, hardware.
   - **Examples**: Amazon EC2, Google Compute Engine, Microsoft Azure VM.

2. **PaaS** (Platform as a Service)
   - **Level**: Platform.
   - **User responsibility**: Application development and management.
   - **Provider responsibility**: Infrastructure, OS, development tools.
   - **Examples**: Google App Engine, Heroku, Microsoft Azure App Service.

3. **SaaS** (Software as a Service)
   - **Level**: Software.
   - **User responsibility**: Using the application.
   - **Provider responsibility**: Everything (infrastructure, application, security).
   - **Examples**: Gmail, Dropbox, Salesforce, Microsoft Office 365.

4. **FaaS** (Function as a Service) / Serverless
   - **Level**: Function execution.
   - **User responsibility**: Individual code blocks and logic.
   - **Provider responsibility**: Scaling, infrastructure, execution.
   - **Examples**: AWS Lambda, Google Cloud Functions, Azure Functions.

---

### Considerations for Cloud Deployment

1. **Security**:
   - Use strong SSH keys and restrict IP access.
   - Enable two-factor authentication for cloud management.
   - Regular security updates (OS and applications).

2. **Backup and Recovery**:
   - Create snapshots of configurations and data.
   - Utilize automatic backup tools provided by the cloud platform.

3. **Cost Management**:
   - Monitor resource usage and shut down unused VMs.
   - Use cost-effective options like spot instances.

4. **Long-Term Scalability**:
   - Transition to container technologies (e.g., Docker, Kubernetes).
   - Leverage serverless technologies for future needs.

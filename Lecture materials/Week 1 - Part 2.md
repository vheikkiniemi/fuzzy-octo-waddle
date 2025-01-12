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

## Introduction to Web Service

### Web service
- What is a Web Service?
  - A service that provides websites or applications to users over the network.
  - Typically uses HTTP/HTTPS protocols for communication.
- Goals
  - Deliver dynamic or static content to clients (e.g., browsers, mobile apps).
-  Key components:
    1. Client (User)
    2. Server
    3. Data transfer via protocol (TCP/UDP, usually port 80 or 443)

### Basic Architecture

1. Client–Server Model
    - **Client** (e.g., browser or mobile app) sends requests to the server:
      - Uses a specific protocol and port.
      - Typically located in different physical locations → Introduces latency in data transfer.
    - **Server** processes the request and returns a response:
      - Processing consumes resources → Adds latency.
      - Delivering the response also introduces delay.
2. Components
    - **Web Server**: Handles HTTP requests (e.g., Nginx, Apache).
    - **Application Logic**: Implemented using programming languages (e.g., Node.js, Deno, Python).
    - **Database**: Stores and retrieves data (e.g., PostgreSQL, MongoDB).

### Web Service Development Stages

1. Design
    - Define the service's goals and features.
    - Select technologies (e.g., backend/frontend frameworks and databases).
2. Implementation
    - Create a server to handle requests.
    - Design and code frontend and backend logic.
    - Develop API interfaces (REST/GraphQL).
3. Testing
    - Test functionality, security, and performance.
4. Deployment
    - Host the service on a web server or in the cloud (e.g., AWS, Azure, Vercel).

### Tools and Technologies

- Frontend Technologies
  - **Core**: HTML, CSS, JavaScript.
  - **Frameworks**: React, Angular, Vue.js.
- Backend Technologies
  - **Core**: Node.js, Deno, Python (Django/Flask), Ruby on Rails.
- Databases
  - **Relational**: PostgreSQL, MySQL.
  - **NoSQL**: MongoDB, Redis.
- API Interfaces
  - REST, GraphQL.
- Hosting
  - Cloud platforms: AWS, Google Cloud, Azure.
  - Services like Heroku or Vercel.

### Key Considerations

1. Security
    - Use HTTPS.
    - Protect input data (e.g., prevent SQL injections).
    - Implement user authentication (e.g., OAuth).
2. Scalability
    - Design the service to scale with the user base.
    - Use load balancers and caching.
3. Maintenance
    - Keep the server and libraries up to date.
    - Monitor logs and performance.

## On-Premise VM and Web Service Deployment

### Introduction to Web Service Deployment on a Virtual Machine
- What is a Virtual Machine (VM)?
  - A virtual environment that behaves like a physical computer.
  - Hosted using virtualization software (e.g., VirtualBox, VMware, Hyper-V).
- Why Use a Virtual Machine?
  - Isolated development environment.
  - Easy to manage and replicate.
  - Can simulate different operating systems and server environments.
  - Cost-effective → No usage-based fees (unlike cloud).
  - Ideal for various tests (functionality, performance, security).
  - Located nearby physically → Minimal data transfer delays.
  - Essential for security testing in a controlled environment.
- Goals
  - Deploy a web service on a local VM to simulate a real server environment.

### Steps to Set Up and Prepare a Virtual Machine

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

### Developing and Transferring a Web Service to a VM

1. **Develop the Application**:
    - Create a locally functioning application (frontend + backend).
    - Test the application thoroughly before transferring.

2. **Transfer the Application to the Virtual Machine**:
    - Copy files using SCP, SFTP, or Git.
    - Install application dependencies (e.g., `npm install`, `pip install`).

3. **Configure the Server**:
    - Set up the web server to route traffic to the application.
    - If needed, create a `systemd` service for automatic startup.

### Deploying a Web Service in a Virtual Machine

1. **Start the Application**:
    - Test the service locally within the virtual machine (e.g., `curl http://localhost`).

2. **Enable Access for External Devices**:
    - Configure VM network settings (bridged/NAT + port forwarding).
    - Open necessary ports in the firewall (e.g., `sudo ufw allow 80`).

3. **Test External Access**:
    - Verify that the service is accessible from the host machine or other devices (e.g., `curl http://<vm-ip>`).

### Key Considerations and Tips

1. **Maintenance**:
    - Regularly update the operating system and software (`apt update && apt upgrade`).
    - Ensure logs are collected and monitored.

2. **Performance**:
    - Optimize resource usage for the VM (CPU, RAM, I/O).
    - Use caching mechanisms (e.g., Redis, Nginx).

3. **Security**:
    - Use strong passwords and restrict access with SSH keys.
    - Enable HTTPS (e.g., with Let's Encrypt).

4. **Backups and Snapshots**:
    - Create a snapshot before major changes.
    - Back up critical files regularly.


## Additional Resources
- [VirtualBox](https://www.virtualbox.org/)
- [Debian](https://www.debian.org/)
- [Netstat on Debian](https://ultahost.com/knowledge-base/install-netstat-debian/)
- [Using PuTTY for SSH Keys](https://www.techtarget.com/searchsecurity/tutorial/How-to-use-PuTTY-for-SSH-key-based-authentication)
- [Installing Nginx on Debian](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-debian-11)


## Cloud and Web Service Deployment

### Different Cloud Service Models

1. **`IaaS` (Infrastructure as a Service)**
    - **Level**: Infrastructure.
    - **User responsibility**:
        - Operating system, applications, security.
    - **Provider responsibility**:
        - Virtual machines, storage, networks, hardware.
    - **Examples**:
        - Amazon EC2, Google Compute Engine, Microsoft Azure VM.

2. **`PaaS` (Platform as a Service)**
    - **Level**: Platform.
    - **User responsibility**:
        - Application development and management.
    - **Provider responsibility**:
        - Infrastructure, operating systems, development tools.
    - **Examples**:
        - Google App Engine, Heroku, Microsoft Azure App Service.

3. **`SaaS` (Software as a Service)**
    - **Level**: Software.
    - **User responsibility**:
        - Usage through the application.
    - **Provider responsibility**:
        - All infrastructure, application, and security.
    - **Examples**:
        - Gmail, Dropbox, Salesforce, Microsoft Office 365.

4. **`FaaS` (Function as a Service) / Serverless**
    - **Level**: Function-level execution.
    - **User responsibility**:
        - Individual code blocks and their logic.
    - **Provider responsibility**:
        - Scaling, infrastructure, execution.
    - **Examples**:
        - AWS Lambda, Google Cloud Functions, Azure Functions.

- **Summary of Differences**:
    - `IaaS`: Freedom to manage infrastructure.
    - `PaaS`: Faster development without infrastructure management.
    - `SaaS`: Ready-to-use software.
    - `FaaS`: Pay only for execution without managing servers.

### Introduction to Web Service Deployment on a Cloud Virtual Machine (IaaS)

- **Cloud Virtual Machine (VM)**:
    - A virtual machine hosted by a cloud provider (e.g., AWS, Google Cloud, Azure).
    - Offers scalability, flexibility, and quick deployment.

- **Why Use Cloud Services?**
    - Easy resource allocation and scalability.
    - Pay-as-you-go pricing.
    - Access to global services and data centers.

- **Examples of Use Cases**:
    - Static websites, dynamic applications, API services.

### Selecting a Cloud Provider and Preparing a VM

1. **Choose a Cloud Provider**:
    - AWS EC2: General-purpose virtual machines.
    - Google Cloud Compute Engine: Integration with other GCP services.
    - Azure Virtual Machines: Easy integration with Microsoft services.

2. **VM Configuration**:
    - Select the operating system (e.g., Ubuntu, CentOS).
    - Allocate resources (CPU, RAM, storage).

3. **Network Settings**:
    - Create a virtual network.
    - Configure firewalls and allow necessary ports (e.g., 80, 443).

### Transferring and Configuring a Web Service on a Cloud VM

1. **Transfer the Application to the VM**:
    - Use SSH, SCP, or SFTP for file transfer.
    - Alternatively, use tools like Git.

2. **Install Dependencies**:
    - E.g., Node.js, Python, Apache/Nginx, database software.

3. **Configure the Web Server**:
    - E.g., Configure Nginx to route requests to the application.
    - Use caching to improve performance.

4. **Start the Service**:
    - Test locally to ensure it works in the cloud environment.

### Deploying and Managing a Web Service in the Cloud

1. **DNS Configuration**:
    - Point the domain to the VM's public IP address.

2. **SSL/TLS Certificates**:
    - Use services like Let's Encrypt to enable HTTPS.

3. **Load Balancing and Scalability**:
    - Implement the cloud provider's load balancer (e.g., AWS ELB).
    - Utilize auto-scaling to handle increased user traffic.

4. **Monitoring and Management**:
    - Collect logs and performance data using cloud tools (e.g., CloudWatch, Stackdriver).

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

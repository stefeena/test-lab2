# On premise deployment

```mermaid
graph TD;
    A[React Frontend] -->|API Calls| B[Flask Web Server];
    B -->|Database Queries| C[PostgreSQL Database];
    C -->|Data| B;
    B -->|Data| A;
```

The Mermaid diagram represents a web application architecture with three main components: React Frontend, Flask Web Server, and PostgreSQL Database. In this diagram, the React Frontend sends API calls to the Flask Web Server to request data. The Flask server processes these requests and interacts with the PostgreSQL Database through database queries to fetch or update data. The database returns the data to the Flask server, which then sends it back to the React frontend. This flow illustrates the interaction between the client-side and server-side components, emphasizing how they communicate and exchange data in the application.

# IaaS deployment architecture

```mermaid
graph TD
  A[Client] -->|Requests| B[Load Balancer]
  B -->|Secures traffic| F[Security Group & Firewalls]
  F -->|Distributes traffic| C[Flask Web Server VM]
  
  C -->|Serves API and Static Files| D[React Frontend VM]
  C -->|Accesses| E[PostgreSQL Database VM]
  
  D[React Frontend VM]--> E[PostgreSQL Database VM]

  E -->|Data| J[Backup Service]
  E -->|Backup and Restore| J

  E -->|Protected by| F

  subgraph Azure Private Cloud
    B
    F
    C
    D
    E
    
    J
    
  end
```

The below  Mermaid diagram outlines a web application architecture that includes a client interface, a load balancer, security measures, a Flask web server, a React frontend, a PostgreSQL database, and a backup service, all hosted within an Azure Private Cloud. Clients initiate requests to the load balancer, which secures and distributes the traffic to the Flask web server. This server handles API requests and serves static files while accessing the PostgreSQL database for data management. The React frontend interacts with the Flask server to present information to users and can also query the database directly. Additionally, the PostgreSQL database is connected to a backup service to ensure data protection and recovery. Overall, this structure emphasizes both functionality and security, ensuring a robust web application environment.

# Deployment using PaaS

```mermaid
graph TD;
    User[User]
    Firewall[Firewall]
    Docker[Docker]
    ReactApp[React App Running on Vercel]
    FlaskApp[Flask App Azure VM]
    Azure[PostgreSQL on Azure]
    API[API Calls]

    User --> Firewall
    Firewall --> ReactApp
    ReactApp -->|API Requests| API
    API --> FlaskApp
    FlaskApp --> Azure
    API --> ReactApp
    ReactApp -->|Response| Docker
    Firewall -->|Response| User

    subgraph Docker
    FlaskApp     
    end
```
The Mermaid diagram depicts a web application architecture in an Azure Private Cloud. It features a Client that sends requests to a Load Balancer, which secures and distributes traffic to a Flask Web Server. The server handles API requests and interacts with a PostgreSQL Database. The React Frontend communicates with both the Flask server and the database. Security is enforced through Firewalls, and a Backup Service ensures data protection. This setup emphasizes robust functionality and security for the application.

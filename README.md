# Project: Full Stack Web Application with Docker, NGINX, and NGINX Proxy Manager

## Overview
This project showcases the setup of a full-stack web application using Docker. It includes a PostgreSQL database, a backend application, and a frontend application. NGINX is integrated as a reverse proxy, and NGINX Proxy Manager is used to manage SSL certificates and streamline the handling of multiple services.

## Project Structure
The project comprises the following main components:

- **PostgreSQL**: A relational database for persistent data storage.
- **Backend**: The server-side application, typically a REST API.
- **Frontend**: The client-side application, usually built with a modern framework.
- **NGINX**: A web server used as a reverse proxy for handling requests and serving static files.
- **NGINX Proxy Manager**: A tool for managing SSL certificates and configuring reverse proxy settings through a user-friendly interface.
- **Adminer**: A web-based database management tool for PostgreSQL.

## Docker Compose Configuration
Here’s an overview of the Docker Compose file and the rationale behind the configurations.

### Services

- **Postgres**
  - **Image**: `postgres:13`
  - **Environment Variables**: Sets up the database name, user, and password.
  - **Volumes**: Data is persisted in a Docker volume to ensure database data is not lost upon container restarts.
  - **Ports**: Exposes port 5432 for external database interaction.

- **Backend**
  - **Build**: Specifies the backend directory for building the Docker image.
  - **Volumes**: Mounts the backend directory to the container, allowing live changes during development.
  - **Ports**: Exposes port 8000 for accessing the backend API.
  - **Depends On**: Ensures the PostgreSQL service starts before the backend.
  - **Environment Variables**: Configures details such as database connection and CORS settings.

- **Frontend**
  - **Build**: Specifies the frontend directory for building the Docker image.
  - **Command**: Runs the frontend application using `npm run dev` for development purposes.
  - **Volumes**: Mounts the frontend directory to the container.
  - **Ports**: Exposes port 5173 for accessing the frontend application.

- **NGINX**
  - **Image**: Uses the latest NGINX image.
  - **Volumes**: Mounts the custom NGINX configuration file.
  - **Depends On**: Ensures both frontend and backend services start before NGINX.

- **Adminer**
  - **Image**: Uses the latest Adminer image for database management.
  - **Restart Policy**: Always restarts to ensure high availability.
  - **Ports**: Exposes port 8080 for accessing Adminer.
  - **Environment Variables**: Sets the default database server for Adminer.

- **Proxy Manager**
  - **Image**: Uses the latest NGINX Proxy Manager image.
  - **Restart Policy**: Configured to restart unless manually stopped.
  - **Ports**: Exposes ports 81, 80, and 443 for accessing the NGINX Proxy Manager dashboard and handling HTTP/HTTPS traffic.
  - **Volumes**: Mounts directories for proxy configuration and SSL certificates.
  - **Depends On**: Ensures NGINX and Adminer services start before NGINX Proxy Manager.

### Volumes
- **postgres_data**: Ensures that PostgreSQL data is stored persistently.

## The Decision to Use NGINX and NGINX Proxy Manager

## How to Run the Project

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/BashDee/devops-stage-2.git
   cd your-repo
   ```

2. **Build and Run Docker Containers:**

   ```bash
   docker-compose up --build
   ```

3. **Access the Applications:**

   - **Frontend**: [https://chacehng.mooo.com]
   - **Backend**: [http://chacehng.mooo.com:8000]
   - **Adminer**: [http://db.chacehng.mooo.com]
   - **Nginx Proxy Manager**: [https://proxy.chacehng.mooo.com]

4. **Configure Domains and SSL in NGINX Proxy Manager:**
   - Log in using the default credentials (`admin@example.com` / `changeme`).
   - Add your domains and configure SSL as needed.

## Conclusion
This project demonstrates a robust setup for a full-stack web application using Docker, NGINX, and NGINX Proxy Manager. The configuration ensures scalability, security, and ease of management, making it suitable for both development and production environments.
## Project Overview

This project automates the configuration and deployment of a containerized e-commerce web application using Ansible on a Vagrant-provisioned Ubuntu server. The application includes three major components: a frontend, a backend, and a MongoDB database. Each component is containerized and managed using Docker.


---

## Why This Order of Execution?

The Ansible playbook `main.yml` was designed to follow a logical, dependency-aware sequence of tasks to ensure a smooth deployment process:

1. **Install System Dependencies and Docker**  
   Before any containers can be deployed, Docker and its dependencies must be available on the system. This is done in the `common` role.

2. **Clone the Project Repository**  
   The application source code is cloned into the VM so the Docker build context is available for container setup.

3. **Start MongoDB Container**  
   The backend service depends on MongoDB. To ensure the backend has a working database connection, the MongoDB container is started first.

4. **Start Backend Container**  
   After the database is running, the backend can be deployed and connected to the MongoDB service.

5. **Start Frontend Container**  
   Finally, the frontend is started. It connects to the backend to fetch and display product data.

Each component is implemented as a separate Ansible role to ensure modularity, reusability, and clear separation of responsibilities.

---

## Roles Explained

### 1. `common`
- **Purpose**: Prepares the system by installing Docker and essential dependencies.
- **Modules Used**:
  - `apt`: To install required packages.
  - `docker_container`, `docker_image`: To manage Docker after installation.

### 2. `mongodb`
- **Purpose**: Starts a MongoDB container for data storage.
- **Modules Used**:
  - `docker_container`: Launches the MongoDB container.
- **Notes**: Ensure volume mounting is used for persistence (can be improved).

### 3. `backend`
- **Purpose**: Deploys the backend server as a containerized service.
- **Modules Used**:
  - `docker_container`: Builds and runs the backend container.
- **Dependencies**: Must run after MongoDB is up.

### 4. `frontend`
- **Purpose**: Launches the frontend user interface for the e-commerce platform.
- **Modules Used**:
  - `docker_container`: Builds and runs the frontend container.

---

## Ansible Concepts Used

### Roles
Roles are used to split the project into manageable parts (frontend, backend, database, common setup).

### Tasks
Each role includes a `tasks/main.yml` file where the actual steps are defined using Ansible modules.

### Variables (To Improve)
Currently, variables are defined inline in tasks. This could be improved by using `vars/` folders or global `group_vars`/`host_vars` to make the playbook more dynamic.

### Tags & Blocks (To Improve)
The current playbook does not use `tags` or `blocks`. These would be helpful for:
- Running specific parts of the playbook
- Better debugging
- Task grouping

---

## Additional Notes

- **Testing Add Product Functionality**: Once the application is deployed, navigate to the frontend URL and use the form to test adding a product. The backend should persist the product data in MongoDB.
- **MongoDB Persistence**: Consider adding Docker volumes in the `mongodb` role to ensure data persists across container restarts (e.g., mount `/data/db`).


This project demonstrates the practical use of Ansible to automate the deployment of a containerized application. It aligns with modern DevOps practices and can be further improved by:
- Adding variable files
- Using blocks and tags
- Implementing persistent MongoDB storage
- Documenting or integrating optional Terraform support

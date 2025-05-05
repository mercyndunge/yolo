
# Overview
This project involves the containerization and deployment of a full-stack Yolo e-commerce application using Docker, Vagrant, and Ansible. The application consists of a frontend, backend, and a MongoDB database, all running as Docker containers.

# Requirements
1. Install the following tools on your host machine:
   - [Vagrant](https://developer.hashicorp.com/vagrant/downloads)
   - [VirtualBox](https://www.virtualbox.org/)
   - [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

2. Clone this repository:
   ```bash
   git clone https://github.com/mercyndunge/yolo.git
   cd yolo

# How to Launch the Application
1. start the vagrant machine:
     vagrant up

2. Run the Ansible playbook to configure the Vagrant machine and deploy the application:
     ansible-playbook -i inventory.yml playbook.yml

3. Access the application:
    Frontend: http://localhost:5678


4. Project Structure
    Vagrantfile: Defines the virtual machine configuration.
    playbook.yml: Ansible playbook to configure the VM and deploy the application.
    inventory.yml: Ansible inventory file specifying the target VM.
    docker-compose.yaml: Defines the Docker services for the application.
    roles/: Contains Ansible roles for better task organization.

5. Ansible Playbook Tasks
   The Ansible playbook performs the following tasks:
    Updates and upgrades apt packages.
    Installs required packages (Docker, Docker Compose, Git).
    Adds the vagrant user to the docker group.
    Clones the application repository.
    Starts the application using Docker Compose.
    
6. Docker Setup
    The application is containerized using Docker Compose.
      Services:
      -Frontend: React application running on port 3000.
      -Backend: Node.js application running on port 5000.
      -The application consists of a frontend, backend, and a MongoDB database, all running as Docker containers.

7. Install the following tools on your host machine:
    Vagrant
    VirtualBox
    Ansible

8. Clone this repository:
     git clone https://github.com/mercyndunge/yolo.git
     cd yolo

9. How to launch the application
     Start the Vagrant machine:
       vagrant up

    Run the Ansible playbook to configure the Vagrant machine and deploy the application:
       ansible-playbook -i inventory.yml playbook.yml

    Access the application:
      Frontend: http://localhost:5678

10. Project Structure
     Vagrantfile: Defines the virtual machine configuration.
     playbook.yml: Ansible playbook to configure the VM and deploy the application.
     inventory.yml: Ansible inventory file specifying the target VM.
     docker-compose.yaml: Defines the Docker services for the application.
     roles/: Contains Ansible roles for better task organization.
     README.md: Documentation for the project.
     
11. Ansible Playbook Tasks
     The Ansible playbook performs the following tasks:
     Updates and upgrades apt packages.
     Installs required packages (Docker, Docker Compose, Git).
     Adds the vagrant user to the docker group.
     Clones the application repository.
     Starts the application using Docker Compose.

12. Docker Setup
    The application is containerized using Docker Compose.
      Services:
       Frontend: React application running on port 3000.
       Backend: Node.js application running on port 5000. 
       Database: MongoDB running on port `




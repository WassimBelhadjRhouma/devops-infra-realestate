# Project Concept – Real Estate Web App with DevOps Lifecycle

## Short summary
In this project I want to run a small real estate web application and apply DevOps practices around it.  
The goal is to set up the full life cycle: build, test, deploy and run the app in a Linux environment.  
The application allows users to create and view property listings (simple CRUD) and uses PostgreSQL as a backing service.

I will use one Ubuntu virtual machine with Docker and Docker Compose, and I will automate builds and deployments using GitHub Actions.

---

## Application
I will implement a small open-source real estate listings app myself and publish it on GitHub.  
For the assignment I will use a fork or clone of that repository as required.

**Planned tech stack:**
- **Backend:** Node.js with Express  
- **Frontend:** React with TypeScript  
- **Styling:** Tailwind CSS  
- **Database:** PostgreSQL  

I will follow basic 12-Factor principles such as using environment variables, stateless containers, and PostgreSQL as an external backing service.

---

## Infrastructure & hosting
All services will run on a **local Ubuntu VM**.

**Runtime stack:**
- Ubuntu Linux  
- Docker and Docker Compose  
- One VM hosting both test and production environments  

**Services I will provision on the VM:**
- Application container  
- PostgreSQL container (with a persistent volume)  
- Nginx reverse proxy  
- Optional monitoring (health endpoint + cAdvisor/Prometheus/Grafana if time allows)

---

## Repositories
I will use two Git repositories:

### 1. Application repository
- Contains the React/Express/PostgreSQL app  
- Includes a Dockerfile  

### 2. Infrastructure repository
- Contains this concept (`concept.md`)  
- Docker Compose files for test and production  
- Environment files (`.env.test`, `.env.prod`)  
- GitHub Actions CI/CD workflows  
- Provisioning steps or notes  
- Monitoring configuration (if added)

The application repo represents the app itself; the infra repo defines how it is deployed and operated.

---

## Environments and separation
The project uses two environments:

- **Test**  
- **Production**

Both run on the same VM but are kept separate through:

- different Compose project names  
- separate Compose files  
- separate environment variables  
- different hostnames on the reverse proxy  

For example:
- Test: `realestate-test.local`  
- Prod: `realestate.local`

I will map these hostnames to the VM’s IP using `/etc/hosts`.

The test environment will receive automatic deployments, while production will only be updated manually.

---

## CI/CD and lifecycle
**Version control & automation:**
- GitHub for both repositories  
- GitHub Actions for CI/CD  
- Docker Hub or GitHub Container Registry for images  

**Artifact:**  
A Docker image of the application.

**Pipeline overview:**
- **Build:** install dependencies, build the app, build Docker image  
- **Test:** backend tests (and optional frontend tests)  
- **Publish:** push the Docker image to a registry  
- **Deploy to test:** automatic rollout on the VM  
- **Deploy to production:** same steps, but triggered manually  

This ensures every change goes through build → test → automatic test deployment, and production is only updated when I approve it.

---

## Provisioning
Provisioning steps for a fresh machine:

1. Create an Ubuntu VM in VirtualBox  
2. Install Docker and Docker Compose  
3. Set up a non-root user and SSH keys for the CI/CD connection  
4. Clone the infrastructure repository  
5. Start the test and production stacks using Docker Compose  

The goal is that the whole setup can be recreated easily on any Linux machine.

---

## Why I chose these technologies
- **React + Node.js:** technologies I already know, allowing me to focus on DevOps  
- **PostgreSQL:** reliable backing service that I want to learn deeper  
- **Ubuntu + Docker Compose:** simple and common setup for small deployments  
- **GitHub Actions:** integrated and easy to use for automating CI/CD  

---

## Learning goals
With this project I want to:

- learn how to containerize a full-stack app  
- build a practical CI/CD pipeline  
- understand how to separate environments and manage configuration  
- gain experience in deploying and operating a small application on Linux  

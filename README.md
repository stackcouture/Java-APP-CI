### DevSecOps CI Pipeline with Jenkins

![View Only](https://img.shields.io/badge/license-view--only-red)
![Status](https://img.shields.io/badge/usage-portfolio%20only-blue)

---

### Overview

The pipeline ensures **code quality, SBOM generation, container security, supply chain integrity and GitOps-driven deployment**.

---

## Demo Flow

![Demo GIF](https://github.com/stackcouture/devsecops-gitops-automation/raw/main/demos/jenkins-ci.gif)

---
### Prerequisites

Ensure the following are installed and configured before running the pipeline:

- Jenkins with required plugins:
  - Pipeline  
  - Docker & Docker Pipeline  
  - GitHub Integration  
  - Slack Notification  
  - SonarQube Scanner  
- **AWS CLI** configured with appropriate IAM permissions  
- **Amazon ECR** repository created  
- **Amazon EKS** cluster running with worker nodes  
- **ArgoCD or FluxCD** set up for GitOps CD  
- **SonarQube** server (running & accessible from Jenkins)  
- **Dependency Track** server (for SBOM ingestion)  
- **Cosign** installed on Jenkins agents  

---

### Tools & Technologies

- **CI/CD**: Jenkins Shared Libraries
- **Build/Test**: Maven, JUnit, Jacoco
- **Code Quality**: SonarQube
- **Security**: Trivy, Snyk, Cosign, Dependency Track
- **Containerization**: Docker
- **Registry**: Amazon ECR
- **Orchestration**: Kubernetes (Amazon EKS)
- **GitOps**: ArgoCD
- **Notifications**: Slack, AI Reports

---

### How to Run

#### Build locally
```bash
mvn clean install
```
#### Run locally
```bash 
mvn spring-boot:run
```
#### Run containerized
```bash
docker build -t java-webapp -f Dockerfile-dev .
docker run -p 8080:8080 java-webapp
```

#### The application will be available at:
👉 http://localhost:8080

---

### Pipeline Stages

The pipeline executes the following stages:

1. **Init & Checkout**  
   Fetch application code from GitHub repository.

2. **Build + Test**  
   Compile the project with Maven, run unit tests, and generate code coverage reports.

3. **Javadoc**  
   Generate Java documentation.

4. **SBOM + FS Scan**  
   - Generate SBOM (CycloneDX format).  
   - Perform file system scan using Trivy.  
   - Upload SBOM to Dependency Track.  

5. **SonarQube Analysis**  
   Run static code analysis, check against quality gates.

6. **Docker Build**  
   Build Docker image for the Spring Boot application.

7. **Pre-Push Security Scans**  
   - Scan local image with Trivy and Snyk before pushing.  

8. **ECR Push**  
   Push Docker image to **Amazon Elastic Container Registry (ECR)**.

9. **Cosign Signing**  
   Sign the Docker image for supply chain security.

10. **Post-Push Security Scans**  
    Re-validate the pushed & signed image.

11. **Confirm YAML Update**  
    Manual approval step before GitOps update.

12. **Update Deployment Files**  
    Update GitOps repository with the new image digest.

13. **Deploy App**  
    GitOps (ArgoCD/FluxCD) applies the deployment into **Amazon EKS**.

14. **Security Report**  
    Generate a consolidated **AI-powered HTML Security Report**  
    (Trivy, Snyk, SonarQube, SBOM summary).

15. **Cleanup**  
    Remove temporary Docker artifacts and free up Jenkins agent space.

---

### Features

- Full CI/CD pipeline with **DevSecOps best practices**  
- Automated **SBOM generation** & ingestion into Dependency Track  
- **Container signing & verification** with Cosign  
- **Multi-layer security scans** (Trivy, Snyk, SonarQube)  
- **GitOps-based deployment** with ArgoCD/FluxCD  
- **AI-powered HTML report** summarizing all scan results 

--- 

### License

This project is provided under a **view-only** license for review and portfolio purposes.  
See the [LICENSE](./LICENSE) file for details.

---
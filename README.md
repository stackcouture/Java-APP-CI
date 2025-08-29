# Java WebApp – CI/CD with Jenkins, Docker, ECR, and GitOps

## 📌 Overview
This project is a **Spring Boot web application** with a fully automated **CI/CD pipeline** built using **Jenkins**.  
The pipeline ensures continuous integration, security scanning, and GitOps-based deployment into **Amazon EKS**.

## Key Features
-  **Build & Test** with Maven (JUnit + Jacoco coverage)
-  **Generate Javadocs** for API documentation
-  **SBOM Generation** & upload to **Dependency Track**
-  **Security Scanning** using **Trivy** and **Snyk**
-  **SonarQube** Quality Gate enforcement
-  **Docker Image Build** & push to **Amazon ECR**
-  **Image Signing** with **Cosign** (supply chain security)
-  **Post-Push Security Validation** (Trivy + Snyk)
-  **GitOps Workflow** – auto-update of CD repo with new image digest
-  **Deployment** into **Amazon EKS** via GitOps
-  **Notifications** via **Slack** + AI-based Security Reports

## Tools & Technologies
- **CI/CD**: Jenkins Shared Libraries
- **Build/Test**: Maven, JUnit, Jacoco
- **Code Quality**: SonarQube
- **Security**: Trivy, Snyk, Cosign, Dependency Track
- **Containerization**: Docker
- **Registry**: Amazon ECR
- **Orchestration**: Kubernetes (Amazon EKS)
- **GitOps**: ArgoCD
- **Notifications**: Slack, AI Reports

## Workflow Stages
1. **Code Checkout** (from GitHub repo)
2. **Build & Test**  
   - Compile with Maven  
   - Run Unit + Integration Tests  
   - Generate Jacoco Coverage Report  
3. **Quality & Security**  
   - Run SonarQube analysis  
   - Generate SBOM (CycloneDX) and upload to Dependency Track  
   - Run Trivy + Snyk scans  
4. **Artifact & Image**  
   - Build Docker image  
   - Push to Amazon ECR  
   - Sign with Cosign  
5. **Post-Push Validation**  
   - Rescan image with Trivy + Snyk  
6. **GitOps Update**  
   - Update deployment manifest in GitOps repo with new image digest  
   - Trigger ArgoCD sync  
7. **Deployment** into Amazon EKS  
8. **Notifications**  
   - Slack alerts  
   - AI-generated HTML Security Report  

---
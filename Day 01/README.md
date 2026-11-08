# Day 1: Docker Fundamentals for Kubernetes | CKA Certification Course 2025

## **How Were Development and Deployment Done Before Docker? Why Do We Need Docker? What Challenges Does It Solve?**

![Alt text](/images/1a.png)

Before Docker, the software lifecycle involved several manual and error-prone processes:

### **1. Development**
- Developers manually installed required software and dependencies on their machines.  
- Teams wrote lengthy setup instructions to replicate environments for development, testing, and production.

### **2. Testing**
- Test environments were manually configured to resemble production systems, but differences in configuration often caused problems.  
- Even minor inconsistencies led to bugs that only appeared in production, making testing unreliable.

### **3. Deployment**
- Applications were packaged into `.tar.gz` files or `.zip` archives.  
- Scripts or manual processes were used to copy files, install dependencies, and configure services—leading to human errors and delays.

---

### **Challenges with Traditional Deployment Approaches:**  

1. **Dependency Management:**  
   - Different operating systems, libraries, and configurations across environments lead to inconsistencies.  
   - Example: Development uses **Python 3.4**, but production runs **Python 3.1**, causing compatibility issues.  

2. **Inefficient Resource Usage:**  
   - Running multiple Virtual Machines (VMs) for different applications increases overhead.  
   - Hosting multiple applications on a single VM leads to resource contention.  

3. **Complex & Error-Prone Deployment:**  
   - Manual configurations across development, testing, and production environments introduce human errors.  
   - Each environment may require different settings, leading to deployment failures.  

4. **Lack of Isolation:**  
   - Applications running on the same VM can **conflict** due to shared dependencies, ports, or configurations.  
   - Example: Two applications requiring **different versions of the same library** can lead to unexpected failures.  

**Solution?** → **Docker Containers** 

---

## **What Is Docker?**

![Alt text](/images/1b.png)

Docker revolutionizes development and deployment by introducing **containers**. Let’s compare:

### **Before Docker**
- Applications were **manually loaded** into environments alongside their dependencies, leaving them vulnerable to configuration mismatches between development, testing, and production environments.  
- If your production server had a different setup than your development machine, issues could arise.

### **With Docker**
- Applications, along with their dependencies, are packaged into **containers**.  
- These containers ensure consistency across all environments (development, testing, and production), solving compatibility issues and speeding up the software lifecycle.

---
## **Virtual Machines (VMs) vs Docker Architecture**
1. VM Architecture  
   ``` Physical HW -> Hypervisor -> VM1[OS + App1], VM2[OS + App2]... ```

3. Docker Architecture  
  ``` Physical HW -> Hypervisor -> VM[OS + Docker Engine] -> Docker Engine -> Container1, Container2... ```


| Feature | Virtual Machines (VMs) Setup | Docker Setup (Inside a VM) |
| :--- | :--- | :--- |
| **OS Layering** | Every App requires a dedicated Guest OS | All Containers share a single VM Guest OS |
| **Resource Efficiency** | High overhead (OS duplicated per application) | Low overhead (Shared memory and CPU resources) |
| **Startup Speed** | Slow (Minutes to boot a full virtual machine) | Instant (Seconds to launch a container process) |
| **Isolation Type** | Hardware-level (Enforced by hypervisor) | Process-level (Enforced by Linux namespaces) |
| **Best Match For** | Running entirely different operating systems | Packing microservices inside a secure VM node |


---

## **High-Level Workflow with Docker**

![Alt text](/images/1d.png)

---

## **Low-Level Workflow with Docker**

### **Key Concepts:**
1. **Docker Images:**  
   The blueprints for containers, including code and dependencies.

2. **Docker Containers:**  
   The runnable instances created from images.

3. **Docker Registries:**  
   Storage locations for Docker images, such as Docker Hub.

4. **Docker Engine:**  
   The core component that powers Docker.

---

### **Docker Engine Components**
- **Docker CLI:**  Acts as the dashboard, letting you issue commands.  
- **REST API:** Translates CLI commands (e.g., `docker run`) into HTTP requests for the Docker Daemon. This enables automation and integration with external tools.
- **Docker Daemon:** The “engine” that handles pulling images, building containers, and other core functions.

### **Key Steps in the Workflow:**
1. **Developer writes a Dockerfile** (stored in version control like Git).
2. **Building the image:**  
   - The developer runs `$ docker build`, which creates a **Docker Image** locally.
3. **Pushing the image to a registry:**  
   - The built image is uploaded (`$ docker push`) to a **Docker Registry** (like DockerHub, ECR, ACR, JFrog, Nexus).
4. **Running containers in different environments:**  
   - Other teams (like DevOps) **pull** the image (`$ docker pull`) and deploy it using `$ docker run` in:
     - **Test environment** (VM in purple).
     - **Production environment** (VM in blue).

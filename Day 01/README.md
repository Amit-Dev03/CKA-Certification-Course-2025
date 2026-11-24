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

### **Challenges with Traditional Deployment Approaches:**  (Dependency -> ineffiecient resource utilization -> manual configuration -> lack of isolation)

1. **Dependency Management:**  
   - Different operating systems, libraries, and configurations across environments lead to inconsistencies.  
   - Example: Development uses **Python 3.4**, but production runs **Python 3.1**, causing compatibility issues.  

2. **Inefficient Resource Usage:**  
   - Running multiple Virtual Machines (VMs) for different applications increases overhead.  
   - Hosting multiple applications on a single VM leads to <span title="A VM has a limited amount of CPU, memory, disk I/O, and network capacity. When multiple applications share it, they compete for those resources. For example, a memory-heavy app could use most of the available RAM, leaving another app short of memory and causing it to slow down or crash. This is called resource contention. It can be reduced by setting resource limits, monitoring usage, or separating workloads across VMs or containers.">resource contention</span>.   

3. **Lack of Isolation:**  
   - Applications running on the same VM can **conflict** due to shared dependencies, ports, or configurations.  
   - Example: Two applications requiring **different versions of the same library** can lead to unexpected failures.  

**Solution?** → **Docker Containers** 

---

## **What Is Docker?** (SPISE -> Standardized, portable, isolated, scalable, Effecient)

![Alt text](/images/1b.png)

Docker revolutionizes development and deployment by introducing **containers**. Containers gave us 5 main principles : SPISE. Let’s compare:

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
### **Docker Engine Components**
- **Docker CLI:**  Acts as the dashboard, letting you issue commands.  
- **REST API:** Translates CLI commands (e.g., `docker run`) into HTTP requests for the Docker Daemon. This enables automation and integration with external tools.
- **Docker Daemon:** The “engine” that handles pulling images, building containers, and other core functions.

## OCI
- The Open Container Initiative (OCI) is an open governance project under the Linux Foundation that defines industry-wide, vendor-neutral standards for container formats and runtimes.
- It ensures that containers built with one tool (like Docker) can be stored, distributed, and run by any other compliant tool (like Podman, containerd, or Kubernetes) without vendor lock-in.

## **Docker vs Podman(Daemonless + rootless)**

Docker and Podman both run OCI containers and share most of the same CLI, so the real differences come down to architecture and ecosystem.

### **Architecture**

- **Docker** uses a client-server model. The `docker` CLI talks to `dockerd`, a long-running daemon that traditionally runs as root and manages all containers.
- **Podman** is daemonless. Each container is a child process of the command that started it (forking model), with `conmon` supervising it. No central process to crash or attack.

### **Security**

- **Podman** is rootless by default, so a container escape lands you in an unprivileged user context rather than root. Docker supports rootless mode too, but it isn't the default and is less commonly used.
- **Docker's** root daemon is a bigger attack surface (access to the Docker socket is effectively root on the host).



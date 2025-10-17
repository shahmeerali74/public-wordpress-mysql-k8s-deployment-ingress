**To follow how to do the deployment step by step follow the medium aritcle in more detail**

**Medium** | https://medium.com/@syed.sas74/deploying-a-wordpress-application-with-mysql-on-aks-using-pv-pvc-and-ingress-via-ui-4f078dc3a2df

**Deploying WordPress with MySQL on Azure Kubernetes Service (AKS) using PV/PVC and Ingress**

This project demonstrates how to deploy a WordPress application with a MySQL database inside an Azure Kubernetes Service (AKS) cluster.

It includes setting up Persistent Storage (PV/PVC) for data retention and configuring an NGINX Ingress Controller for secure, external access.

**🚀 Architecture Overview**

The setup contains:

AKS Cluster

WordPress Deployment + Service

MySQL Deployment + Service

PersistentVolumeClaims (PVCs) for both applications

Ingress Controller (NGINX) for external access

Single domain: shahmeer.mndev.site

**📘 Data Flow:**

User → Ingress → WordPress Service → WordPress Pod

WordPress → MySQL Service → MySQL Pod

Both WordPress and MySQL persist data using Azure Managed Disks via Kubernetes PVCs.

🖼️ Architecture Diagram:

<img width="3338" height="1037" alt="diagram-export-17-10-2025-14_31_02" src="https://github.com/user-attachments/assets/0f4a6bd1-09fd-47ab-83a6-17a4d082b9aa" />

**🧩 Step 1: Create Deployment Files**

All YAML deployment files are already available in this repository:

mysql-deployment.yaml

wordpress-deployment.yaml

wordpress-ingress.yaml

Make sure your AKS cluster is deployed and connected through kubectl.

**🐬 Step 2: Deploy MySQL**

Use the MySQL deployment and service file:

- kubectl apply -f mysql-deployment.yaml

This creates:

A PersistentVolumeClaim for MySQL data storage

A MySQL Deployment and ClusterIP Service

**🌐 Step 3: Deploy WordPress**

Deploy the WordPress configuration:

- kubectl apply -f wordpress-deployment.yaml

This will:

Create a PVC for WordPress

Deploy the WordPress container

Expose it through a LoadBalancer for external access

**⚙️ Step 4: Verify Deployments**

- kubectl get pods

- kubectl get svc

Wait until the external IP for WordPress appears.

**🌍 Step 5: Access WordPress**

Navigate to your external IP in the browser:

- http://<EXTERNAL-IP>

You’ll see the WordPress setup page.

**🧭 Step 6: Install NGINX Ingress Controller**

Install Ingress for unified domain routing:

- kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.1/deploy/static/provider/cloud/deploy.yaml

Wait for the pods to be ready:

- kubectl get pods -n ingress-nginx

**🪄 Step 7: Apply Ingress Configuration**

Use the Ingress YAML file to expose WordPress via your domain:

- kubectl apply -f wordpress-ingress.yaml

**Check the Ingress:**

- kubectl get ingress


Once the DNS (shahmeer.mndev.site) points to the Ingress IP, you can access WordPress at:

- https://shahmeer.mndev.site
 
**🧰 Tools Used**

1. Azure Kubernetes Service (AKS)
2. kubectl
3. NGINX Ingress Controller
4. Persistent Volumes / PVCs
5. Azure Managed Disks

**✨ Outcome**

✅ WordPress successfully deployed on AKS with:

1. Persistent storage for both WordPress and MySQL
2. Internal communication between services
3. External domain access via NGINX Ingress

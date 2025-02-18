# MyDello Azure Infrastructure Deployment

## 📌 Overview
This **Azure Resource Manager (ARM) template** automates the deployment of **networking and virtual machines (VMs) for MyDello**.

### **🔹 What This Template Does**
- **Creates a Virtual Network (`MyDello-VNet-1`)** with two subnets (`Subnet1` & `Subnet2`).
- **Deploys a Network Security Group (`MyDello-NSG-Subnet`)** to secure the VMs.
- **Assigns Static Public IPs** for the VMs.
- **Creates two Ubuntu 24.04 LTS VMs (`MyDello-VM-Web-1` and `MyDello-VM-Web-2`)**.
- **Configures Network Rules** to allow:
  - **HTTP traffic (Port 80)** for web access.
  - **SSH access (Port 22)** for administration.

---

## 🚀 **How to Deploy via Azure Portal**
### **1️⃣ Recommended Region**
- The **recommended region** for deployment is:  
  ✅ **`North Europe`** (for best availability and performance).  
- However, **you can use any other region** if preferred.

### **2️⃣ Deployment Steps**
1️⃣ **Sign in to the [Azure Portal](https://portal.azure.com/)**.  
2️⃣ **Go to the "Deploy a Custom Template" page**:  
   - Click **Create a resource** → **Search "Template Deployment"** → Select **Deploy a custom template**.  
3️⃣ **Click "Build your own template in the editor"**.  
4️⃣ **Copy and paste the contents of `combined-deploy.json`** into the template editor.  
5️⃣ **Click "Save"**.  
6️⃣ **Enter the Resource Group Name** → **Use `MyDello-RG` (Recommended)**.  
7️⃣ **Set the Region**:
   - **Recommended**: `North Europe`
   - **Optional**: Choose another region if needed.
8️⃣ **Click "Review + Create"** → Then **"Create"** to start deployment.

---

## 🔗 **Accessing the VMs**
### **1️⃣ Find the Public IPs**
After deployment, go to:  
📍 **Azure Portal** → **Resource Group (`MyDello-RG`)** → **Public IP Addresses**.  

Or run this command in **Azure CLI**:
```sh
az network public-ip list --resource-group MyDello-RG --query "[].{VM: name, PublicIP: ipAddress}" --output table

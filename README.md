# azure-vm-bastion-terraform
Deploy an Azure Virtual Machine with Azure Bastion using Terraform for secure, browser-based SSH/RDP connectivity without exposing public IPs.

---

# Deploy Azure VM with Bastion Using Terraform

This repository provides a step-by-step guide and Terraform configuration to deploy an Azure Virtual Machine (VM) with Azure Bastion for secure remote access.

## **Overview**

This project demonstrates how to deploy the following resources in Azure using Terraform:
- Azure Resource Group
- Virtual Network (VNet) with two subnets (one for the VM, one for Bastion)
- Azure Bastion Host
- Virtual Machine (Linux-based)

Azure Bastion allows secure and seamless RDP or SSH connectivity to your virtual machines through the Azure Portal without exposing public IP addresses on your VM.

---

## **Prerequisites**

Before you begin, ensure you have the following:
1. An active [Azure Subscription](https://azure.microsoft.com/).
2. [Terraform](https://www.terraform.io/downloads) installed on your local machine.
3. [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) installed for authentication.
4. A text editor, such as [VS Code](https://code.visualstudio.com/).

---

## **Steps to Deploy**

### **1. Clone the Repository**

```bash
git clone https://github.com/Curious4Tech/azure-vm-bastion-terraform.git
cd azure-vm-bastion-terraform
```

### **2. Authenticate with Azure**
1. Log in to Azure using the Azure CLI:
   ```bash
   az login
   #Alternatively
    az login --tenant your_tenant_id
   ```
![image](https://github.com/user-attachments/assets/706cac0f-5910-4e0d-b01d-77f722b6e66a)

2. Set your desired subscription if not set in the previous step (**`step 1.`**) or want to change it :
   ```bash
   az account set --subscription "YOUR_SUBSCRIPTION_ID"
   ```

### **3. Initialize Terraform**
Run the following command to initialize Terraform in this directory:
```bash
terraform init
```
![image](https://github.com/user-attachments/assets/8e2cd834-68b7-4071-91a7-08da57e3bc8d)

### **4. Plan the Deployment**
Generate a plan to preview the resources that will be created:
```bash
terraform plan
```

![image](https://github.com/user-attachments/assets/b53385e6-1b06-40ae-94a2-586292f8e112)

### **5. Apply the Configuration**
Deploy the resources by applying the Terraform configuration:
```bash
terraform apply
```
Type **`yes`** when prompted.

---

## **Verify the Deployment**

1. Log in to the [Azure Portal](https://portal.azure.com).
2. Navigate to the resource group created (`rg-bastion-demo`).
3. Confirm the following resources:
   - Virtual Network with two subnets.
   - Public IP for Bastion.
   - Bastion Host.
   - Virtual Machine.

---

## **Connecting to the VM Using Azure Bastion**

### **1. Navigate to the VM in Azure Portal**
1. Open the [Azure Portal](https://portal.azure.com).
2. Go to the **`Resource Group`** you created (e.g., **`rg-bastion-demo`**).
3. Select the **`Virtual Machine`** (e.g., **`linux-vm`**).

### **2. Use Azure Bastion for SSH**
1. In the VM overview page, click on the **Connect** button.
2. Choose **Bastion** from the connection options.
3. Provide the following details:
   - **`Username`**: Use the `admin_username` you specified in the Terraform script (e.g., `azureuser`).
   - **`Password`**: Use the `admin_password` you specified in the Terraform script (e.g., `P@ssw0rd123!`).
4. Click **`Connect`**.

### **3. Secure Connection**
Azure Bastion establishes a secure connection to your VM directly in your browser without requiring a public IP address or additional configuration.

---

## **Terraform Configuration**

The main Terraform configuration is in the `main.tf` file and contains the following:
1. **`Resource Group`**
2. **`Virtual Network`** with two subnets:
   - `subnet-vm`: For the VM.
   - `AzureBastionSubnet`: Required for Azure Bastion.
3. **`Azure Bastion Host`**
4. **`Linux Virtual Machine`**

---

## **Files**

| File       | Description                                         |
|------------|-----------------------------------------------------|
| `main.tf`  | Main Terraform configuration file.                 |
| `variables.tf` | (Optional) Define reusable variables for configuration. |
| `outputs.tf` | (Optional) Export outputs for created resources.  |

---

## **Resource Diagram**

Below is a high-level representation of the architecture:

```
Resource Group
├── Virtual Network (10.0.0.0/16)
│   ├── Subnet: VM Subnet (10.0.1.0/24)
│   ├── Subnet: AzureBastionSubnet (10.0.2.0/24)
├── Bastion Host (Public IP + Bastion Subnet)
├── Virtual Machine (Ubuntu, VM Subnet)
```

---

## **Clean Up**

To delete all resources created by Terraform, run:
```bash
terraform destroy
```
Type **`yes`** to confirm.

-----

## **Conclusion**

Deploying a Virtual Machine with Azure Bastion ensures a secure and efficient way to manage remote access without exposing your VMs to public networks. With Terraform, this process is streamlined and repeatable, making infrastructure as code a powerful tool for managing cloud resources. For any issues or questions, please open an issue in the repository.

Happy coding! 🚀

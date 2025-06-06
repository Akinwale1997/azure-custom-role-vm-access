# 🔐 Azure Custom Role Creation + VM SSH Access (with Free Tier Limitation Handling)

This project demonstrates how to create a Custom Azure Role with limited permissions and assign it to a user using the Azure CLI. It includes all the necessary configuration, screenshots of the implementation steps, and real-world error handling — including what happens when your subscription is on the free tier.

---

## 🧠 Project Goal

Create a Custom Role named "VM Start Stop Reader Role" that allows:
- Starting/stopping a virtual machine
- Reading network interface & IP data
- Viewing subscription resource group details

Then assign that role to a user using the Azure CLI.

---
---

## 📦 Step-by-Step Implementation

### ✅ 1. Launch Cloud Shell
- Used Bash shell in Azure Cloud Shell  
- Verified shell loaded with olarinde [ ~ ]$
![Cloud Shell](./01-cloud-shell-launched.png)

### ✅ 2. Create Custom Role JSON

Opened a new file using nano nm-role.json and pasted this:

`json
{
  "Name": "VM Start Stop Reader Role",
  "IsCustom": true,
  "Description": "Can start, stop VMs and read metrics/network",
  "Actions": [
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/deallocate/action",
    "Microsoft.Compute/virtualMachines/read",
    "Microsoft.Network/networkInterfaces/read",
    "Microsoft.Network/publicIPAddresses/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/metrics/read"
  ],
  "NotActions": [],
  "AssignableScopes": ["/subscriptions/<your-subscription-id>"]
}


### ✅ 3. Custom Role Creation (Output)
![Role Created](./002-Custom-Role-Created-Output.png)

### ✅ 4. JSON Role Output
![Role JSON Output](./03-Custom-Role-Created-output.png)

### ❌ 5. Role Assignment Failure (Free Tier)
![Assignment Failed](./04-role-assignment-falure-free-tier.png)

---

## 🧠 Insight:- free tier subscrption often block custom role assignments unless billing is enabled or upgraded.

---

## 🧠  Real-World Lesson 
This project reflects real troubleshooting;
- How to test Custom Json role definitions
- Catch and resolve errors like subscription/role provider issues
- What happens on free-tier Azure when trying advanced RBAC

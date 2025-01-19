#  Migration of Applications from Azure to Google Cloud Platform (GCP)
## Overview:
This project involves migrating applications, virtual machines, and associated resources from Microsoft Azure to Google Cloud Platform (GCP). The migration aims to enhance performance, reduce costs, and leverage GCP’s advanced capabilities, including better data analytics, machine learning, and improved infrastructure.

## Key Phases in the Migration Process:
**Onboard**: Select and prepare the source VM for migration.

**Replication**: Replicate data from Azure to GCP continuously.

**Set VM Target Details**: Configure the VM settings on GCP (instance type, network, etc.).

**Test-Clone**: Optionally, create a clone of the VM for testing purposes on GCP.

**Cut-Over**: Migrate the source VM to GCP by stopping the source VM, completing a final replication, and creating a production instance on GCP.

**Finalize**: Perform final cleanup after successful migration.

![image](https://github.com/user-attachments/assets/c73b8367-ec4b-455d-8188-1fa2d851c418)

## Steps:
  ## 1. Set Up Google Cloud Platform Free Trial Account:
   **1.1) Navigate to Google Cloud.**
   ![image](https://github.com/user-attachments/assets/357dfcfc-abf4-45aa-b962-8e8b988484c7)

  **1.2) Start the free trial and set up payment details for verification.** 
  ![image](https://github.com/user-attachments/assets/1f94cdc9-d41c-4f92-b99d-6e149f136785)
  
  ![image](https://github.com/user-attachments/assets/27af37f6-8cda-49bf-90ce-5d263bc46f00)
  
  ![image](https://github.com/user-attachments/assets/50991c1c-ddc2-4e62-ad31-705de43fbf10)

  **1.3) Install and configure the Google Cloud CLI for managing cloud services.**
  ![image](https://github.com/user-attachments/assets/2e7c5803-b4cb-4f33-b14f-0ef05cc3678f)
  
  ![image](https://github.com/user-attachments/assets/be2ec663-73a9-435b-a8e4-bda3434b7b8b)
  
  ![image](https://github.com/user-attachments/assets/4f11f73b-0585-46e9-af74-1ce7f5003269)
  
  ![paint](https://github.com/user-attachments/assets/f8ce7235-092b-4d6b-bba1-eef09b36343f)
  
  ![image](https://github.com/user-attachments/assets/78388009-6998-431e-a248-57f39f74efe7)
  
  ![image](https://github.com/user-attachments/assets/3ebcc87a-c283-4655-adfd-94629b448d7c)

## 2. Create Azure Source:
  **2.1) Register an app in Azure for the migration process**
  ![image](https://github.com/user-attachments/assets/bd62e346-9fcd-49f9-b5ef-4aff68963b59)
  
  ![image](https://github.com/user-attachments/assets/4b879e58-e0c1-40c6-ae06-932cd2d1a4cc)

  ![image](https://github.com/user-attachments/assets/696c2f19-b896-43af-b38c-98012d268abc)

  ![image](https://github.com/user-attachments/assets/4ce18ecd-b96c-451b-a72a-f4d27626d5b6)
  
  **2.2) Generate client secret credentials to grant necessary permissions for migration**
   ![image](https://github.com/user-attachments/assets/4c5bc8c4-06e6-45a8-bdc7-7243a47c2c59)

  ![image](https://github.com/user-attachments/assets/dfcc962c-0e9d-42e0-81f7-2d267ed6e8f4)

  **2.3) Create a custom role in Azure and assign the required permissions**
  ![image](https://github.com/user-attachments/assets/1efbff24-beab-49e4-aeb5-f42f022fde55)
  
  
  ![image](https://github.com/user-attachments/assets/ff22b5e4-72ee-44fb-b5cf-f27cf6a77195)
  
  
  ![image](https://github.com/user-attachments/assets/ef100bfc-f7f8-4b71-b05d-c68e4e334a42)
  
  paste the below json file after entering your **SUBSCRIPTION_ID** and hit `Review + Create`.
```json
       {
  "properties": {
        "roleName": "Minimum M2VM permissions role",
        "description": "This role contains the bare minimum of Azure IAM permissions to support M2VM flow",
        "assignableScopes": [
              "/subscriptions/SUBSCRIPTION_ID"
        ],
  "permissions": [
              {
              "actions": [
                    "Microsoft.Resources/subscriptions/resourceGroups/write",
                    "Microsoft.Resources/subscriptions/resourceGroups/read",
                    "Microsoft.Resources/subscriptions/resourceGroups/delete",
                    "Microsoft.Compute/virtualMachines/read",
                    "Microsoft.Compute/virtualMachines/write",
                    "Microsoft.Compute/virtualMachines/deallocate/action",
                    "Microsoft.Compute/disks/read",
                    "Microsoft.Compute/snapshots/delete",
                    "Microsoft.Compute/snapshots/write",
                    "Microsoft.Compute/snapshots/beginGetAccess/action",
                    "Microsoft.Compute/snapshots/read",
                    "Microsoft.Compute/snapshots/endGetAccess/action"
              ],
              "notActions": [],
              "dataActions": [],
              "notDataActions": []
              }
        ]
  }
  }
  ```

![image](https://github.com/user-attachments/assets/66b8e426-052d-4514-bcdb-14291744061f)

![image](https://github.com/user-attachments/assets/d2cadbc4-0a5f-492d-96d6-63828ba4e932)

![image](https://github.com/user-attachments/assets/f097150d-4bd2-4260-b0df-9ac16a6ce6c8)

![image](https://github.com/user-attachments/assets/c2304797-75ec-4694-b435-5eccd8a0fa29)

![image](https://github.com/user-attachments/assets/aeb0384a-ed90-408d-a204-45ac641ec980)

![image](https://github.com/user-attachments/assets/55140ac7-cba6-4814-a362-751bfc8b8374)


## 3. Migration on Google Cloud:
**3.1) Access Google Cloud Console, navigate to Compute Engine, and initiate the migration process.**
![image](https://github.com/user-attachments/assets/c7e5161a-fc6b-4b82-a8bf-6bb667dc3dda)

**3.2) Add Azure as the source cloud.**
![image](https://github.com/user-attachments/assets/bd8833dc-6666-433a-ba6b-2c52e1c12cc0)

![image](https://github.com/user-attachments/assets/b406e0d1-7209-4275-8300-89b8243f7232)

![image](https://github.com/user-attachments/assets/30a20113-acf0-470e-aa7f-63b7a7046fe9)

In 10 to 15 minutes, the source virtual machines will be added, and their status will show activated.
![image](https://github.com/user-attachments/assets/da0eedf9-ea19-4d8a-ad47-ac4982340eff)

**3.3) Select the virtual machines to migrate and initiate the replication process.**
![image](https://github.com/user-attachments/assets/4a3ffcc2-5138-4587-9f1f-b39c4b8de444)
![image](https://github.com/user-attachments/assets/da8c2e09-d66f-48a9-88cd-7e9d803cc466)

**3.4) Set target details for Compute Engine.**
We will Select the VM’s and click on EDIT TARGET DETAILS so that we can perform TEST-CLONE or CUT-OVER.

![image](https://github.com/user-attachments/assets/0e973d5e-b032-4abe-8dc6-a1c34156d095)

![image](https://github.com/user-attachments/assets/5423ada3-6d9c-43c6-906a-d9bfc7b3599f)

![image](https://github.com/user-attachments/assets/6142baac-047e-4a88-9d18-aadd3e8f1130)

![image](https://github.com/user-attachments/assets/061f3e12-465f-4a16-835e-6e0b83e68f79)


**3.5) Perform "Test-Clone" or "Cut-Over" as per the migration strategy.**

![image](https://github.com/user-attachments/assets/9ca2b0b5-f7ac-4542-8cf9-68d15e3a1247)

![image](https://github.com/user-attachments/assets/dd397bb1-4024-46f4-9db0-4c0dfb092f08)

![image](https://github.com/user-attachments/assets/13754034-caf7-460f-97ff-85e8a4b2dd0c)

![image](https://github.com/user-attachments/assets/0093510d-3699-450d-8355-afda85adac0d)




















  

  







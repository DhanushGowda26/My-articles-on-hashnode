---
title: "Storage in Kubernetes"
datePublished: Tue Dec 10 2024 18:30:34 GMT+0000 (Coordinated Universal Time)
cuid: cm4isrbvp000109mj3hpd8c5a
slug: storage-in-kubernetes
tags: aws, azure, kubernetes, devops, storage

---

### **1\. Understanding Key Concepts**

#### **Persistent Volumes (PV)**

* A **Persistent Volume (PV)** is a piece of storage in the Kubernetes cluster that has been provisioned either statically or dynamically. It is a cluster-wide resource that abstracts the underlying physical storage and is managed by Kubernetes.
    
* PVs are **independent of the lifecycle** of any individual Pod that uses the volume. This means they can be reused and are not tied to any specific Pod.
    

#### **Persistent Volume Claim (PVC)**

* A **Persistent Volume Claim (PVC)** is a request for storage by a user. It specifies the amount of storage and the access modes (read/write) required.
    
* PVCs are bound to a PV that meets the request. The Kubernetes scheduler automatically selects the PV that satisfies the claim and binds them together.
    

#### **StorageClass**

* A **StorageClass** defines the type of storage to be used and how it should be provisioned.
    
    * It can specify things like the provisioner (which cloud provider, or storage system), volume type (e.g., SSD, HDD), replication, performance tiers (e.g., Standard, Premium), and other parameters.
        
    * When PVCs are created, they reference a StorageClass that defines how the underlying volume is provisioned and what kind of performance/storage options are available.
        

---

### **2\. Static Provisioning**

**Static provisioning** means that Persistent Volumes (PVs) are pre-created manually by administrators. Users can then request the available PVs by creating Persistent Volume Claims (PVCs).

### **Static Provisioning in Azure (AKS)**

**Storage Options for Static Provisioning in Azure (AKS):**

1. **Azure Managed Disks**  
    Azure Managed Disks are the default disk storage solution. They are scalable and high-performance.
    
    * **Use Case**: Used for applications that require high-performance block-level storage.
        
    * **Types**: Standard HDD, Standard SSD, Premium SSD.
        
2. **Azure Files**  
    Azure Files is a fully managed file share service in the cloud, accessible using the SMB (Server Message Block) protocol.
    
    * **Use Case**: Used for shared file storage where multiple clients may need access, such as for lifting and shifting legacy apps or shared storage.
        

**Steps for Static Provisioning in AKS:**

1. **Create the Azure Disk/Files:**
    
    * Azure disks are created manually through Azure Portal, CLI, or ARM templates.
        
    * For Azure Files, create a file share in the Azure Storage account.
        
2. **Create a Persistent Volume (PV):**
    
    * You need to manually define the PV in Kubernetes by specifying the disk or file share URL.
        
3. **Create Persistent Volume Claim (PVC):**
    
    * After PV creation, users can create PVCs that will bind to the manually created PV.
        

**Example PV for Azure Disk**:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: azure-disk-pv
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  azureDisk:
    diskName: <disk-name>
    diskURI: <disk-uri>
    kind: Managed
    fsType: ext4
```

**PVC Example:**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azure-disk-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
```

---

### **Static Provisioning in AWS (EKS)**

**Storage Options for Static Provisioning in AWS (EKS):**

1. **Amazon EBS (Elastic Block Store)**
    
    * EBS is a scalable and persistent block-level storage service.
        
    * **Use Case**: Used for high-performance applications, databases, or for scenarios where direct block storage is required.
        
2. **Amazon EFS (Elastic File System)**
    
    * Amazon EFS is a scalable and managed file storage system for use with AWS Cloud services and on-premises resources.
        
    * **Use Case**: Shared access to file-based storage across multiple instances.
        

**Steps for Static Provisioning in EKS:**

1. **Create the EBS Volume or EFS:**
    
    * EBS volumes are created manually via AWS Console or CLI.
        
    * EFS filesystems are also created through the AWS Console/CLI and mounted to EC2 instances.
        
2. **Create Persistent Volume (PV):**
    
    * Manually create the PV and reference the EBS volume or EFS filesystem.
        
3. **Create Persistent Volume Claim (PVC):**
    
    * After creating the PV, users can create PVCs to claim the manually created PVs.
        

**Example PV for EBS Volume:**

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: ebs-pv
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  awsElasticBlockStore:
    volumeID: <volume-id>
    fsType: ext4
```

**PVC Example:**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ebs-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
```

---

### **3\. Dynamic Provisioning**

**Dynamic provisioning** refers to Kubernetes automatically provisioning storage for a PVC based on a StorageClass definition. This eliminates the need to manually create PVs.

### **Dynamic Provisioning in Azure (AKS)**

**Storage Options for Dynamic Provisioning in Azure (AKS):**

1. **Azure Managed Disks (Premium SSD, Standard SSD, Standard HDD)**  
    Azure Disks can be dynamically provisioned based on the StorageClass parameters you specify.
    
2. **Azure Files**  
    Azure Files can also be dynamically provisioned using the right StorageClass.
    

**Steps for Dynamic Provisioning in AKS:**

1. **Create a StorageClass**: Define the type of Azure Disk (e.g., Premium SSD).
    
2. **Create a PVC**: When a PVC is created, Kubernetes will automatically provision the storage.
    

**Example StorageClass for Dynamic Provisioning:**

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: azure-disk
provisioner: kubernetes.io/azure-disk
parameters:
  storageaccounttype: Premium_LRS
```

**PVC Example:**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azure-disk-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: azure-disk
```

When this PVC is created, Kubernetes will automatically provision an Azure Disk using the `azure-disk` StorageClass.

---

### **Dynamic Provisioning in AWS (EKS)**

**Storage Options for Dynamic Provisioning in AWS (EKS):**

1. **Amazon EBS (Elastic Block Store)**
    
    * EBS can be dynamically provisioned using the AWS EBS CSI driver.
        
2. **Amazon EFS (Elastic File System)**
    
    * EFS can also be dynamically provisioned using the AWS EFS CSI driver.
        

**Steps for Dynamic Provisioning in EKS:**

1. **Install the CSI Drivers**: Install the **EBS CSI driver** or **EFS CSI driver** on your EKS cluster.
    
2. **Create a StorageClass**: Define the storage options for dynamic provisioning.
    
3. **Create a PVC**: When a PVC is created, Kubernetes will automatically provision the volume based on the StorageClass.
    

**Example for EBS CSI Driver and StorageClass:**

**StorageClass for EBS:**

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-sc
provisioner: ebs.csi.aws.com
parameters:
  type: gp2
```

**PVC Example:**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ebs-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: ebs-sc
```

When this PVC is created, Kubernetes will automatically provision an EBS volume using the `ebs-sc` StorageClass.

---

### **Key Takeaways**

* **PV (Persistent Volume)**: A cluster-wide storage resource provisioned statically or dynamically.
    
* **PVC (Persistent Volume Claim)**: A user’s request for storage, which can be dynamically bound to a PV.
    
* **StorageClass**: Defines the provisioning type (dynamic or static) and other parameters for storage like disk type, replication, etc.
    
* **Static Provisioning**: PVs are created manually and then bound to PVCs. Common for managing storage options like Azure Disks, EBS, or NFS.
    
* **Dynamic Provisioning**: PVs are automatically created by Kubernetes when a PVC is created. It uses StorageClasses to define how volumes are provisioned,
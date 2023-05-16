# 7.1 Managing Pod Volumes
- The YAML definition for the pod has a **volumes** configuration under the **spec** key.

# 7.2 Using Persistent Volumes
- Pod Volumes depend on pods
    * To have storage outlast a Pod, the volume should connect to external storage
    * This can be done from within the Pod, but that would require the developer to know about storage specifics.
    * To decouple storage requirements from Pod development, Persistent Volumes are offered
    * Decoupling is key, and ensures that everybody can focus on their duties.

## 7.2.1 Implementing storage decoupling
- The PersistentVolumeClaim (PVC) is used by the user to claim storage in a declarative way, without worrying about storage specifics
    * e.g. Just specify you need 10 GiB of storage and use different types of storage in your dev and production environments.

- The PersistentVolume (PV) represents the storage resource in the Kubernetes cluster.
    * Administrators can configure the storage statically
    * The Kubernetes cluster can configure storage dynamically using StorageClass

- The PersistentVolumeClaim (PVC) is a kubernetes API object that has a spec that defines required storage properties
    * accessModes: which type of access is required
    * resources: how much storage is required?
    * StorageClassName: which storage class type is required?

- Based on these properties, the PVC will reach out to a PV to bind to specific storage.

- PersistentVolume is the kubernetes object that defines how to connect to external storage and uses different spec attributes
    * capacity: how much storage is available
    * accessMode: which access mode
    * StorageClassName: (optional) how to bind to a specific storage class
    * PersistentVolumeReclaimPolicy: what to do when a corresponding PersistentVolumeClaim is deleted
    * type: which specific storage type to use (nfs, azureDisk, gcePersistentDisk etc)

# 7.3 Setting up Pods to use Persistent Volumes
- Make the PV, and PVC first, and make sure they are specified in the Pod definition

# 7.4 Understanding Dynamic Provisioning
- PVs can be created manually

- Alternatively, PVs can be dynamically provisioned. To dynamically provision a PV, a StorageClass must be referred to in the PVC

- Storage classes are using classes that are defined by the administrator. It is up to the admin to decide what to use to categorize: storage type, backup type, QoS, or something else

- Storage classes, are also using provisioners that connect to a specific storage type. Each provisioner has its own parameters

- A default storage class can be used, alternatively storage classes can be defined manually.

## 7.4.1 Understanding StorageClass Provisioner
- The provisioner is a key element in dynamic storage as it contains the code to create specific storage resources.

- Kubernetes comes with some provisioners, most of which are related to public cloud enironments

- The parameters section in the StorageClass definition contains provisioner-specific parameters and explains how to connect to the actual storage.

- A Default StorageClass can be used to always specify a storage type so that it doesn't have to be defined in the PVC spec anymore

- You'll find Default StorageClasses in specific Managed kubernetes environments, such as AKS

## 7.4.2 Using the Default StorageClass
- Using the Default StorageClass provided by a cluster is simple: nothing has to be specified in the PVC definition.

- Custom StorageClass is used to define a StorageClass resource that binds to specific storage

- You will need to set up the provisioner to allow access to that specific storage (think about cloud credentials)

- Once defined, the custom StorageClass can be accessed from the PVC.

# 7.5 Using ConfigMaps
-  ConfigMap is providing configuration as a separate api object in the kubernetes database, that allows you to insert configuration into a Pod

- The goal of a configmap is separate configuration from code

- ConfigMaps are clear-text, Secrets are base64-encoded

- Different types can be used:
    * Files
    * Directories
    * Literals

- No matter which type is used, all the associated data is stored in the ConfigMap or Secret object.

- Secrets are mainly used to push variables.

# 7.6 Using Secrets
- Kubernetes automatically creates Secrets that contain credentials for accessing the API, and automatically modifies the pods to use this type of Secret.

- Use **kubectl describe pods <podname>** and look for the mount section to see them.

- While creating a secret, the text value must be base64 encoded

- When using **kubectl create secret** this is happening automatically.

- When creating a secret from a YAML file, you'll need to use the **base64** utility to generate the encoded string and use that in the YAML file.

## 7.61 Using Secrets
- From Pods, Secrets are used in the way that ConfigMaps are used
    * Mounted as volumes
    * Imported as variables

# Assignment
Set up a Pod that uses external NFS storage that is provided through a Persistent volume.

# Solution
1. Let's make a test directory which will host our volume.
``mkdir /sample/data && cd /sample/data``

2. Create a file, e.g. index.html. You can put words in there
``sudo sh -c "echo 'Hello from Kubernetes storage' > /mnt/data/index.html"``

3. Now create a Persistent Volume, with the volume at **/sample/data**. See **pv-lab7.yaml**. Create the resource by running the command ```kubectl create -f pv-lab7.yaml```

4. Your PV has been created, and it should have a status of **available**, meaning its not been bounded to a PersistentVolumeClaim yet. Let's make one. See **pvc-lab7.yaml**. Create the resource by running the command ```kubectl create -f pvc-lab7.yaml```

5. After you create the PersistentVolumeClaim, the Kubernetes control plane looks for a PersistentVolume that satisfies the claim's requirements. If the control plane finds a suitable PersistentVolume with the same StorageClass, it binds the claim to the volume. You can check by running the command ``kubectl get pvc pv-claim-lab7``

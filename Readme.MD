## Introduction:
This is the IBM Cloud Private for Data Open API offering that enables users to programmatically operate with the Information Governance Catalog and Analytics services allowing for creating robust applications surrounding data catalog and deployment management. 

## Prerequisites:
IBM Cloud Private for Data

## Installing the chart
Follow the steps to have the ICP4D Open API application up and running on your cluster.
1.	SSH to the ICP4D cluster
```bash
ssh root@<ICP4D-cluster-master-node>
```

2.	After successfully logging in to your cluster, pull the ICP4D Open API docker image
```bash
docker pull ibmicp4d/icp4d-open-apis:v1
```

3.	Push the docker image from your node to the docker registry using the following commands
    
    a. Tag the image
    ```bash
    docker tag ibmicp4d/icp4d-open-apis:v1 mycluster.icp:8500/zen/icp4d-api:v1
    ```
    b. Push the image to the private image registry.
    ```bash
    docker push mycluster.icp:8500/zen/icp4d-api:v1
    ```
    
4.	Clone the github repository IBM-ICP4D/icp4d-apis to receive a copy of the helmchart. Browse to the repo directory
```bash
git clone https://github.com/IBM-ICP4D/icp4d-apis.git
cd icp4d-apis
```
    
5.	Install the helmchart archive with the following command
```bash
helm install helmchart --name icp4d-open-api --namespace zen --tls
```

Run the following kubectl commands to verify the deployment.
```bash
kubectl get svc -n zen|grep icp4d-open-api
kubectl get pod -n zen|grep icp4d-open-api
kubectl describe pod <the_pod_it_made> -n zen
```

You can now access the ICP4D Open API's with the following link
[https://`ICP4D-cluster`:31843/icp4d-api/docs](https://%60icp4d-cluster%60:31843/icp4d-api/docs)

## Uninstalling the chart
To uninstall/delete the icp4d-openapi deployment:
```bash
helm delete --purge icp4d-open-api --tls
```

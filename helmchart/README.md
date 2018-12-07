## Introduction:

This chart can deploy the ICP4D Open API to enable users to programmatically operate with the Information Governance Catalog and Machine Learning components in IBM Cloud Private for Data. 

## Prerequisites:

IBM Cloud Private for Data v1.2 or higher

## Installing the chart
1. Pull the ICP4D Open API docker image
```bash
docker pull ibmicp4d/icp4d-open-apis:v1
```

2. Login to the private docker registry
```bash
docker login mycluster.icp:8500 -u <username> -p <password>
```

3. Push the docker image from your local file system to your docker image registry using the following commands
    
    a. Tag the image
    ```bash
    docker tag icp4d-api:v1 mycluster.icp:8500/zen/icp4d-api:v1
    ```
    b. Push the image to the private image registry.
    ```bash
    docker push mycluster.icp:8500/zen/icp4d-api:v1
    ```

4. Make sure that the values.yaml in helmchart folder has the same tag as the downloaded/newly created docker image
5. Install the helmchart archive with the following command
```bash
helm install helmchart --name icp4d-openapi --namespace zen --tls
```

Run the following kubectl commands to verify the deployment.
```
kubectl get svc -n zen|grep helmchart
kubectl get pod -n zen|grep helmchart
kubectl describe pod <the_pod_it_made> -n zen
```

You can now access the ICP4D Open API's with the following link
https://`ICP4D-cluster`:31843/icp4d-api/docs

## Uninstalling the chart

To uninstall/delete the `icp4d-openapi` deployment:
```bash
$ helm delete icp4d-openapi --tls
```

# Linode Kubernetes Engine Helm Chart Deployment Of Mongodb and Mongo-Express

This project aims to deploy a scalable MongoDB cluster along with Mongo Express for easy administration on Linode Kubernetes Engine (LKE). The setup includes deploying MongoDB using Helm charts (StatefulSet) and exposing it via an Ingress with the help of Linode NodeBalancer.

## Prerequisites
Before deploying this project, ensure you have the following:

- Access to Linode Kubernetes Engine (LKE) with a managed cluster.
- Linode Block Storage or any other storage class compatible with your Kubernetes cluster for persistent storage.
- Basic knowledge of Kubernetes concepts like Deployments, Services, and Ingress.
- Helm installed on your local machine to deploy MongoDB.

## Installation Steps

### 1. Deploy MongoDB

    ```bash
    helm install mongodb oci://registry-1.docker.io/bitnamicharts/mongodb
    ```

### 2. Deploy Mongo Express

    ```bash
    kubectl apply -f mongo-express-service.yaml
    kubectl apply -f mongo-express-deployment.yaml
    ```

### 3. Configure Ingress
Apply the Ingress YAML file with appropriate host configurations:

    ```bash
    kubectl apply -f mongo-express-ingress.yaml
    ```

Replace <linode-nodebalancer-host-ip> with the actual Linode NodeBalancer IP address.

## Accessing Mongo Express
Once the deployment is successful and the Ingress is configured, you can access Mongo Express using the assigned hostname or IP address. Open a web browser and navigate to:

    ```bash
    http://<linode-nodebalancer-host-ip>/
    ```

## Cleanup
To clean up the resources, simply delete the deployed components:

    ```bash
    kubectl delete deployment mongo-express
    kubectl delete service mongo-express-service
    helm uninstall mongodb
    ```

## Customization
- Adjust the MongoDB replica count, storage class, and other configurations in the mongodb-helm-values.yaml file as per your requirements.
- Modify the Ingress annotations or configurations in mongo-express-ingress.yaml to suit your networking setup.

## Support
For any issues or further assistance, feel free to reach out to Linode support or consult the Kubernetes documentation.

## Disclaimer
Ensure proper backups and security measures are in place before deploying any production workloads. Linode and Kubernetes provide robust tools, but proper configuration and monitoring are essential for a stable environment.
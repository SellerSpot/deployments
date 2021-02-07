# This folder contains Deployements and corresponding service for applications.

## Points to Remember

1. Make sure to specify the namespace the deployment and service should be applied. (we could explicitly give in command, but specifying it in the same yaml file is fail safe.)

    **Note :** Make sure that both deployment and service have same namespace - otherwise service cannot find pod to provision service.

    **Deployment Block**

    ```yaml
    metadata:
    name: <deployment-name>
    namespace: <namespace-for-deployment>
    ```

    **Service Block**

    ```yaml
    metadata:
    name: <service-name>
    namespace: <namespace-for-service>
    ```

2. Make sure to check the following items in the configuration file.

   **Deployment Block**

   ```yaml
   spec:
        containers:
            - name: container
            image: <fill-required-image-name>
            imagePullPolicy: Always
   ```

   **Service Block**

   ```yaml
   spec:
     type: NodePort
     ports:
       - port: <exposed-port-from-deployment>
   ```

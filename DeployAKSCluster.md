# Provisioning a New AKS Cluster

In this guide, we will walk through the steps to provision a new AKS cluster using Azure CLI (bash)

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- Azure CLI installed on your machine
- Azure subscription and appropriate permissions
- Kubernetes knowledge

## Steps

**Step 1**: Log in to Azure CLI using the following command:
    ```bash
    az login
    ```

**Step 2 (Optional)** checking out which Kubernetes versions are available in your region

```bash
az aks get-versions --location <location> --output table
```
![image](https://github.com/apsessoms/Containers-K8s/assets/99392512/bb73c30b-0bca-4447-af16-157f4cceab48)


**Step 3**: Set the Azure subscription you want to use:
    ```bash
    az account set --subscription <subscription_id>
    ```

**Step 4**: Create a resource group for your AKS cluster:
    ```bash
    az group create --name <resource_group_name> --location <location>
    ```

If you recieve an error that says "An RSA key file or key value must be supplied to SSH key value." The error message you're seeing when trying to create the AKS Cluster indiciates that the command is missing an SSH key, which is required for the AKS nodes. Azure uses SSH keys to manage secure access to the nodes in your Kubernetes cluster. Use the following command to generate an SSH key pair while creating the AKS cluster:



```bash
az aks create --resource-group $resource --name $aksName --kubernetes-version 1.24.9 --generate-ssh-keys
```

The **$resource** environment holds the resource group name. 

The **$aksName** environment holds the AKS cluster name. 

The **--generate-ssh-keys** flag is used to generate an SSH key pair for the AKS cluster. 

The **--kubernetes-version** flag is used to specify the Kubernetes version for the AKS cluster. 

**Step 5**: Create the AKS cluster:
    ```bash
    az aks create --resource-group <resource_group_name> --name <cluster_name> --node-count <node_count> --node-vm-size <vm_size> --generate-ssh-keys
    ```

**Step 6**: Connect to the AKS cluster:
    ```bash
    az aks get-credentials --resource-group <resource_group_name> --name <cluster_name>
    ```

**Step 7**: Verify the cluster is running:
    ```bash
    kubectl get nodes
    ```

**Step 8**: Clean up (optional):
    ```bash
    az group delete --name <resource_group_name> --yes --no-wait
    ```

That's it! You have successfully provisioned a new AKS cluster.

## Conclusion

In this guide, we covered the steps to provision a new AKS cluster using Azure CLI. You can now start deploying and managing your applications on the cluster.

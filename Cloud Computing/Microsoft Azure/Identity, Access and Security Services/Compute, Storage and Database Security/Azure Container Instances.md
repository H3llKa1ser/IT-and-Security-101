# Configure security for Azure Container Instances (ACIs)

Azure Monitor provides insight into the compute resources used by your containers instances. This resource usage data helps you determine the best resource settings for your container groups. Azure Monitor also provides metrics that track network activity in your container instances.

## Preview Limitations

At this time, Azure Monitor metrics are only available for Linux containers.

## Available Metrics

Azure Monitor provides the following metrics for Azure Container Instances. These metrics are available for a container group and individual containers. By default, the metrics are aggregated as averages.

1) CPU Usage measured in millicores.

2) One millicore is 1/1000th of a CPU core, so 500 millicores represents usage of 0.5 CPU core.

3) Memory Usage in bytes.

4) Network bytes received per second.

5) Network bytes transmitted per second.

## Get metrics - Azure portal

When a container group is created, Azure Monitor data is available in the Azure portal. To see metrics for a container group, go to the Overview page for the container group. Here you can see pre-created charts for each of the available metrics.

![image](https://github.com/user-attachments/assets/7ffa3e51-268e-4c6b-a1ca-e946305448e6)

In a container group that contains multiple containers, use a dimension to display metrics by container. To create a chart with individual container metrics, perform the following steps:

In the Overview page, select one of the metric charts, such as CPU.

Select the Apply splitting button, and select Container Name.

![image](https://github.com/user-attachments/assets/dc06c161-9e15-4ba1-bdfd-b6e172b3a09a)

## Get metrics - Azure CLI

Metrics for container instances can also be gathered using the Azure CLI. First, get the ID of the container group using the following command. Replace <resource-group> with your resource group name and <container-group> with the name of your container group.

    CONTAINER_GROUP=$(az container show --resource-group <resource-group> --name <container-group> --query id --output tsv)

Use the following command to get CPU usage metrics.

    az monitor metrics list --resource $CONTAINER_GROUP --metric CPUUsage --output table

Change the value of the --metric parameter in the command to get other supported metrics. For example, use the following command to get memory usage metrics.

    az monitor metrics list --resource $CONTAINER_GROUP --metric MemoryUsage --output table

For a multi-container group, the containerName dimension can be added to return metrics per container.

    az monitor metrics list --resource $CONTAINER_GROUP --metric MemoryUsage --dimension containerName --output table

New-AzVm `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVM" `
    -Location "eastus" `
    -VirtualNetworkName "myVNet" `
    -SubnetName "mySubnet" `
    -SecurityGroupName "myNSG" `
    -PublicIpAddressName "myPublicIP"
    from azure.identity import DefaultAzureCredential
from azure.mgmt.compute import ComputeManagementClient

credential = DefaultAzureCredential()
compute_client = ComputeManagementClient(credential, subscription_id)

vm = compute_client.virtual_machines.begin_create_or_update(
    resource_group_name="myResourceGroup",
    vm_name="myVM",
    parameters={
        "location": "eastus",
        "properties": {
            "hardwareProfile": {
                "vmSize": "Standard_DS2_v2"
            },
            "osProfile": {
                "adminUsername": "adminuser",
                "adminPassword": "P@ssw0rd"
            }
        }
    }
).result()
using Microsoft.Azure.Management.Compute;
using Microsoft.Azure.Management.Compute.Models;

ComputeManagementClient computeClient = new ComputeManagementClient(new DefaultAzureCredential());

VirtualMachine vm = new VirtualMachine(
    location: "eastus",
    hardwareProfile: new HardwareProfile(vmSize: VirtualMachineSizeTypes.StandardDS2V2),
    osProfile: new OSProfile(
        adminUsername: "adminuser",
        adminPassword: "P@ssw0rd"
    )
);

computeClient.VirtualMachines.StartCreateOrUpdate(
    resourceGroupName: "myResourceGroup",
    vmName: "myVM",
    parameters: vm
);

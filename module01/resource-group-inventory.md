# CIT 386 Module 1 - Resource Group Inventory

## Access Note

I was unable to access the shared Azure resource group through the Azure portal. I discussed the access issue with my professor and focused on understanding the concepts behind the resources used by an Azure virtual machine.

I was able to successfully connect to VM01 through SSH using PuTTY. This confirmed that the virtual machine was running and accessible.

Because I could not view the resource group, the inventory below is a conceptual example of resources normally used with an Azure virtual machine. I am not listing these as the actual resources in the shared resource group.

## Azure VM Resources

| Resource Type | Purpose |
|---|---|
| Virtual Machine | Runs the operating system and applications. |
| Managed Disk | Stores the VM operating system and data. |
| Network Interface | Connects the VM to the Azure network. |
| Virtual Network | Provides the private network for Azure resources. |
| Subnet | Provides a smaller network inside the virtual network. |
| Network Security Group | Controls allowed and blocked network traffic. |
| Public IP Address | Allows the VM to be reached from outside the Azure network. |

## How They Work Together

The virtual machine uses a managed disk to store its operating system and data.

The network interface connects the VM to a subnet. The subnet is part of the virtual network.

A Network Security Group controls network traffic. For example, SSH uses TCP port 22.

A public IP address can allow a user outside the Azure network to connect to the VM. I was able to use PuTTY and SSH to connect to VM01.

## VM Dependencies

The VM depends on other Azure resources to work correctly.

- The managed disk provides storage.
- The network interface provides network connectivity.
- The subnet and virtual network provide networking.
- The Network Security Group provides traffic rules.
- A public IP can provide remote Internet access to the VM.

## Costs When the VM Is Stopped

Stopping a VM does not always stop every Azure charge.

Managed disks can continue costing money because Azure is still storing the VM's data.

Some public IP address configurations can also continue to have a cost when the VM is not running.

The exact charges depend on how the Azure resources are configured.

## What I Learned

I learned that an Azure virtual machine is not just one resource. It depends on storage, networking, and security resources to operate.

I also learned that stopping a VM does not necessarily stop all Azure costs because some resources continue to exist even when the VM is not running.
ms.ContentId: 71a03c62-50fd-48dc-9296-4d285027a96a
title: Setup Windows Containers in a local VM

# Preparing Windows Server Technical Preview for Windows Containers

In order to create and manage Windows Server Containers, the Windows Server 2016 Technical Preview environment must be prepared. This guide will walk through configuring Windows Server Containers in a virtual machine running locally with Hyper-V.

To run Windows Server Containers in Azure instead, follow [these instructions](./azure_setup.md).
 
## Requirements

* Hyper-V is enabled
* 14GB available (so you can download Server Core and a base image)
* Administrator permissions

** Why do I need Hyper-V? **  
Windows Server Containers do not require Hyper-V. However, this guide and all of the set-up scripts we're providing assume you're running containers in a Hyper-V virtual machine. It's easier to get going in a virtual machine with Hyper-V.

## Set up a new container host on a new virtual machine
There are a few different components necessary for running Windows Server Container, however we have a script that will pull all of these together for you. The following steps will guide you through the automated creation of a new virtual machine configured as a Windows Server Container Host.

1. Download configuration script from – http://updatelocation .
2. Launch a PowerShell session as Administrator.
3. Run the following command to begin an automated deployment of the container host. This example will create a Virtual Machine named CONTAINERHOST with an administrative password or Password12.

  ```powershell
  .\New-ContainerHost.ps1 -VmName CONTAINERHOST -Password Password12
  ```
4. When the script begins you will be asked to read and accept licensing terms.

  ```
  Before installing and using the Windows Server Technical Preview 3 with Containers virtual machine you must:
      1. Review the license terms by navigating to this link: http://aka.ms/WindowsServerTP3ContainerVHDEula
      2. Print and retain a copy of the license terms for your records.
  By downloading and using the Windows Server Technical Preview 3 with Containers virtual machine you agree to such
  license terms. Please confirm you have accepted and agree to the license terms.
  [N] No  [Y] Yes  [?] Help (default is "N"): Y
  ```
This script will then begin to download and configure the Windows Server Container components. This process will take quite some time due to the large download.  
Once finished your Virtual Machine will be configured and ready to create and manage Windows Server Containers with both PowerShell and Docker.

> Note:  If you recieve this message:  
  ```
  Currently, your container is not connected to the network.
  Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>
  ```
  
  You already have set up an external switch and should manually it to your virtual machine.

5. Launch your new virtual machine with VM Connect.  `CONTAINERHOST` is the VMName you used with the `New-ContainerHost` script.
  
  ``` PowerShell
  vmconnect.exe localhost CONTAINERHOST
  ```
  
  The VM should connect to this screen:
  ![](./media/ContainerHost.png)
  
6.  Enter your password.  This is the password you used with the `New-ContainerHost` script.

Now you have a Windows Server Core virtual machine running Docker and Windows Server Containers!
  
Jump to the following quick starts to begin containerizing applications and managing Windows Server Containers.

The Docker and PowerShell guides both walk through containerizing a web server and performing equivelant management tasks.  Use whichever toolset you prefer.

[Quick Start: Windows Server Containers and PowerShell](./manage_powershell.md)  
[Quick Start: Windows Server Containers and Docker](./manage_docker.md)  

-------------------

[Back to Container Home](../containers_welcome.md)
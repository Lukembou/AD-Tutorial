# AD-Tutorial
This project outlines the setup of a Windows 10 virtual machine connected to a Windows Server 2019 domain controller using VirtualBox. It details the installation, configuration of DHCP for IP address management, and domain joining processes, demonstrating how to create a mini corporate network for testing and learning purposes.


# Setting Up a Windows 10 Virtual Machine in VirtualBox

## Introduction

- **Objective**: Create a Windows 10 virtual machine (VM) in VirtualBox with an internal network to connect to a DHCP server.
- **Environment**: Simulating a corporate network setup that includes a Windows Server 2019 Domain Controller.

## Prerequisites

- **VirtualBox Installed**
- **Windows 10 ISO File**
- **Windows Server 2019 with DHCP Role Installed**
- **Network Configuration Diagram** (for reference)

## Step 1: Setting Up Windows Server 2019

1. **Install Windows Server 2019 ISO**:
   - Follow the installation prompts and select the appropriate server edition.

2. **Configure the Server**:
   - Set a static IP address.
   - Enable the DHCP Server role through **Server Manager**.
  ![Install AD DS]!(https://github.com/Lukembou/AD-Tutorial/blob/main/2024-09-22%2020_00_10-Window.png?raw=true)


3. **Create a DHCP Scope**:
   - Define a scope to manage IP address distribution.
   - Set options like default gateway and DNS servers.

## Step 2: Create a New Virtual Machine in VirtualBox

1. **Open VirtualBox**.
2. Click on **New** to create a new VM.
3. **Name the VM**: `Client 1`.
4. **Type**: Windows.
5. **Version**: Windows 10 (64-bit).
6. **Memory**: Allocate RAM (4GB recommended).
7. **Hard Disk**: Create a new virtual hard disk (VDI format).

## Step 3: Configure VM Settings

1. Go to **Settings**.
2. Navigate to **Advanced**:
   - Enable **Shared Clipboard**.
3. Go to **System**:
   - Adjust **Processor** settings if necessary.
4. Go to **Network**:
   - Set **Adapter 1** to **Internal Network**.
5. Click **OK** to save settings.

## Step 4: Add Windows 10 ISO

1. **Double Click** on the created VM.
2. Click **Settings** > **Storage**.
3. Click on **Empty** under Controller: IDE.
4. Browse to the **Windows 10 ISO** and select it.
5. Click **Start** to boot from the ISO.

## Step 5: Install Windows 10

1. Click **Next** and choose "Install Now".
2. Select **I don’t have a product key**.
3. Choose **Windows 10 Pro** and click **Next**.
4. Accept the license terms and choose **Custom Installation**.
5. Proceed with the installation (this may take time).

## Step 6: Initial Configuration

1. During setup, choose **United States** as the region.
2. Opt for **Limited Setup** to avoid creating a Microsoft account.
3. Create a local user (e.g., username: `User`).
4. Disable unnecessary options during the setup.

## Step 7: Verify Network Configuration

1. Open **Command Prompt** and run `ipconfig`.
   - Check for an IP address and default gateway.
2. If no default gateway:
   - Access the Domain Controller and check DHCP settings.
   - Ensure the **Router option** is configured with the Domain Controller's IP.
   - Restart the DHCP service.

## Step 8: Verify Internet Connectivity

1. Back in the Windows 10 VM, run `ipconfig /renew`.
2. Check connectivity by pinging **google.com**.
3. Confirm you can ping the Domain Controller (e.g., `mydomain.com`).

## Step 9: Rename the Computer and Join Domain

1. Right-click **Start** > **System**.
2. Click **Rename this PC** > **Advanced**.
3. Enter new name (e.g., `Client1`) and Domain (`mydomain.com`).
4. Input domain credentials when prompted.

## Step 10: Check Active Directory

1. On the Domain Controller, go to **Active Directory Users and Computers**.
2. Verify that the new computer (`Client1`) appears in the Computers container.
3. Check **DHCP** for leases; confirm the new client is listed.

## Step 11: Log into the Domain

1. On the Windows 10 VM, log out and use the domain credentials to log in.
2. Confirm successful login and access to resources.

## Use Cases in a Work Environment

- **Employee Onboarding**: Automate the creation of user accounts for new hires.
- **Secure Access**: Allow employees to connect to the corporate network securely.
- **Centralized Management**: Manage users and computers from a single domain controller.
- **Network Resource Access**: Enable seamless access to shared drives and applications.

## Conclusion

- Successfully set up a Windows 10 VM on an internal network.
- Configured DHCP and domain settings for network connectivity.
- Demonstrated use of a corporate network environment for secure operations.

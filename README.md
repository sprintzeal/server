# Turning an Old PC into a NAS Server

This guide will walk you through converting an old PC into a Network Attached Storage (NAS) server using Proxmox and Open Media Vault (OMV).

## Requirements
1. Old PC
2. USB Flash Drive (at least 4GB)
3. External or additional internal hard drives (for storage)
4. Internet connection

## Step 1: Download the Necessary Software
1. **Proxmox VE**
   - [Proxmox Download](https://www.proxmox.com/en/downloads)

2. **Rufus**
   - [Rufus Download](https://rufus.ie/)

3. **Open Media Vault (OMV)**
   - [Open Media Vault Download](https://www.openmediavault.org/?page_id=77)

## Step 2: Prepare the USB Flash Drive with Proxmox

1. **Download Proxmox**: Visit the Proxmox download page and download the ISO file.
   
2. **Download and Install Rufus**:
   - Go to the Rufus website and download the latest version.
   - Install and open Rufus.

3. **Create a Bootable USB with Proxmox**:
   - Insert your USB flash drive into your PC.
   - In Rufus, select your USB drive under "Device".
   - Click "Select" and choose the Proxmox ISO file you downloaded.
   - Ensure "Partition scheme" is set to MBR and "File system" is FAT32.
   - Click "Start" and wait for the process to complete.

## Step 3: Install Proxmox on the Old PC

1. **Boot from USB**:
   - Insert the USB drive into the old PC and power it on.
   - Access the BIOS/UEFI settings (usually by pressing F2, F12, Delete, or Esc during startup) and set the USB drive as the primary boot device.

2. **Install Proxmox**:
   - Follow the on-screen instructions to install Proxmox.
   - Select the appropriate hard drive for the installation (this will be your system drive).
   - Complete the installation and remove the USB drive when prompted.

## Step 4: Set Up Proxmox

1. **Initial Configuration**:
   - Boot the PC with Proxmox installed.
   - Open a web browser on another device and navigate to [https://192.168.1.19:8006](https://192.168.1.19:8006/#v1:0:=qemu%2F101:4:::::8::).
   - Log in with the following credentials:
     - Username: `root`
     - Password: `sprintzeal@24`

     - ![image](https://github.com/user-attachments/assets/8fb71f8e-8500-4e19-bf69-d68d8a5a3b59)


2. **Change the Default Password**:
   - Navigate to `Datacenter` > `Permissions` > `Users`.
   - Change the root password.

## Step 5: Create a Virtual Machine for OMV

1. **Download OMV**: Visit the Open Media Vault download page and download the ISO file.

2. **Upload OMV ISO to Proxmox**:
   - In the Proxmox web interface, navigate to `Datacenter` > `Storage` > `ISO Images`.
   - Upload the OMV ISO file.

3. **Create a New VM**:
   - Click `Create VM` and follow the wizard to create a new virtual machine.
   - Assign appropriate resources (CPU, RAM, and storage) to the VM.
   - Select the OMV ISO as the boot disk.

4. **Install OMV**:
   - Start the VM and follow the on-screen instructions to install OMV.
   - Select the virtual hard drive for the installation.
   - Complete the installation and reboot the VM.

## Step 6: Set Up OMV

1. **Initial Configuration**:
   - Boot the VM with OMV installed.
   - Open a web browser on another device and navigate to the IP address assigned to your OMV VM.
   - Log in with the default credentials:
     - Username: `admin`
     - Password: `openmediavault`

2. **Change the Default Password**:
   - Navigate to `System` > `General Settings` > `Web Administrator Password`.
   - Enter and confirm your new password.

## Step 7: Prepare Storage Drives

1. **Attach Storage Drives to Proxmox VM**:
   - In the Proxmox web interface, navigate to `Datacenter` > `Node` > `VM`.
   - Attach additional storage drives to the OMV VM.

2. **Configure Storage in OMV**:
   - In the OMV web interface, navigate to `Storage` > `Disks`.
   - Verify that your storage drives are detected.

3. **Create File Systems**:
   - Go to `Storage` > `File Systems`.
   - Click `Create`, select the appropriate drive, and choose the file system type (e.g., EXT4).
   - Mount the file system once it is created.

4. **Set Up Shared Folders**:
   - Navigate to `Access Rights Management` > `Shared Folders`.
   - Click `Add` to create a new shared folder.
   - Configure the folder's name, path, and permissions.

5. **Configure SMB/CIFS**:
   - Go to `Services` > `SMB/CIFS`.
   - Enable the service and configure the workgroup, description, and shares.

## Step 8: Access Your NAS

1. **Connect to Your NAS**:
   - On your networked devices (PC, Mac, etc.), open a file explorer and navigate to the NAS IP address or hostname.
   - You should see the shared folders you created in OMV.

2. **Map Network Drives**:
   - For easier access, you can map the shared folders as network drives on your devices.

## Additional Resources

- [YouTube Video Guide](https://youtu.be/isIIiqBEqRU?si=rhOOmpomS2CnnN6q)

## Admin Panel Access
- Open your browser and type: `sprintzealstorage.local`
- ![image](https://github.com/user-attachments/assets/bccae2b8-4c6a-4679-9d2c-830890af0ff9)

## Creating a User in the OMV Panel

1. Click the `Users` option.
   ![image](https://github.com/user-attachments/assets/0df44bec-2053-4ec6-90e3-d19487a2592a)

2. Click the `+` option.
   ![image](https://github.com/user-attachments/assets/6739ad0c-31ef-4650-9165-7cd62259b3e3)

3. Input the username and password.
   ![image](https://github.com/user-attachments/assets/5c83d65d-8e8a-42ec-9427-f692a37b54b4)

4. Click the `Apply Changes` button after saving.
   ![image](https://github.com/user-attachments/assets/e83a2d26-bdc2-457c-b536-8cbb34d9d6c6)

## Monitoring Storage Usage

- Navigate to `Storage` to see the usage.
![image](https://github.com/user-attachments/assets/8a32b441-cd83-4a07-9ba1-0a575da563fd)

## Using the Server

1. Click `Network`.
![image](https://github.com/user-attachments/assets/43e8c03f-3e47-4608-891c-dc19f3519457)

2. Select the server name.
![image](https://github.com/user-attachments/assets/ba5d4956-da4e-4b61-bc27-4d74e476d0fd)

3. Enter the username and password.
![image](https://github.com/user-attachments/assets/22c8de2a-13d8-4424-95a6-c96fa46b64b6)

4. Drag and drop files and folders to transfer and store them on the server.
![image](https://github.com/user-attachments/assets/56087680-eb4f-4dc1-8e72-d52b17f12276)

Now everyone connected to the same router or network can access your files.
![image](https://github.com/user-attachments/assets/47fc2e25-59d7-41e1-b90e-16872cf58e2e)

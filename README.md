# Linux Virtualization Host Setup (QEMU/KVM)

## Objective
To enable virutalization on a host running Bazzite Linux by implementing dedicated logical storage and configuring a QEMU/KVM hypervisor. This setup will serve as the foundational infrastructure for future labs.

## Skills Learned
- **Storage Administration:** Managed disks using `fdisk` to create logical partitions.
- **Linux File System Management:** Formatted volumes with `ext4` and implemented persistent mounting via `/etc/fstab` with UUID identification.
- **System Administration:** Resolved `systemd` mound conflicts using `daemon-reload` and managed Linux user groups for hardware-level access.
- **Security Practices:** Verified installation media integrity using SHA-256 checksums and configured directory permission via `chown`.
- **Hypervisor Troubleshooting:** Diagnosed and resolved VM boot failures related to virtualized hardware mapping (SATA CDROOM boot priority).

## Tools Used
- **Host OS:** Bazzite Linux (Fedora-based, Immutable).
- **Partitioning:** `fdisk`, `lsblk`.
- **Hypervisor:** QEMU/KVM with `virt-manager`.
- **Package Management:**`rpm-ostree` (Layered installation).
- **CLI Utilities:** `systemctl`, `sha256sum`, `nano`, `chown`.

# Taken Steps
The following sections document the process used to complete this project, including the challenges encountered and the solutions implemented.
<br/>
## Step 1. Creating the partition

First, I identified the available disk space that would be allocated for virtualization storage:
<img width="755" height="252" alt="Pasted image 20260407202403" src="https://github.com/user-attachments/assets/d52af78a-011f-45f1-a05f-1b0c4098ca8e" />
<br/>
<br/>
While mounting the partition, I encountered the following error:
<img width="721" height="108" alt="Pasted image 20260408203925" src="https://github.com/user-attachments/assets/44199598-688e-46d9-a130-4656529ff2f7" />
<br/>
<br/>
Reviewed the `/etc/fstab` configuration after identifying outdated mount references maintained by `systemd`.
<img width="691" height="305" alt="Pasted image 20260421203314" src="https://github.com/user-attachments/assets/c446f6c9-3b4c-41b3-8c6b-d12ce73898e3" />
<br/>
<br/>
Reloaded the `systemd` daemon to apply the updated mount configuration successfully.
<img width="721" height="108" alt="Pasted image 20260408211008" src="https://github.com/user-attachments/assets/555cd3c9-d71f-4e38-b330-51d13b5720cd" />
<br/>
<br/>
Updated directory ownership to ensure proper access permissions for future virtualization workloads.
<img width="721" height="76" alt="Pasted image 20260408213611" src="https://github.com/user-attachments/assets/c26e1b26-7c62-4055-836b-900ff997268b" />
<br/>
<br/>
## Step 2. Installing QEMU/KVM and Virtual Machine Manager

Verified hardware virtualization support and confirmed KVM modules were loaded correctly.
- `lscpu | grep virtualization`
- `lsmod | grep kvm_amd`
  
<img width="554" height="34" alt="Pasted image 20260410155813" src="https://github.com/user-attachments/assets/5fe174fb-771a-4aa0-ba33-a9e1420fbaad" />
<br/>
<img width="481" height="49" alt="Pasted image 20260410155929" src="https://github.com/user-attachments/assets/d8c3f47a-2809-4066-ab09-799f8408907a" />
<br/>
<br/>
Confirmed successful installation of all virtualization packages and supporting dependencies.
<img width="825" height="443" alt="Pasted image 20260410162007" src="https://github.com/user-attachments/assets/18979b64-c2f0-4a77-93df-dfd389900284" />
<br/>
<br/>
The needed tools were successfully installed:
<img width="859" height="545" alt="Pasted image 20260410164808" src="https://github.com/user-attachments/assets/5f6121a9-4f67-4e10-83e1-4c5a9d898bb9" />
<br/>
<br/>

## Step 3. Create a Kali VM
> Verified the Kali Linux ISO integrity before deployment using the official SHA-256 checksum.
<br/>
<br/>
Created a checksum file using the value published on the Kali Linux website.
<img width="828" height="72" alt="Pasted image 20260412232528" src="https://github.com/user-attachments/assets/1cbc74f6-4b82-4e34-aaa7-5d6badbec372" />
<br/>
<br/>
Validated the downloaded ISO by comparing its generated checksum against the official value.
<img width="828" height="72" alt="Pasted image 20260412232800" src="https://github.com/user-attachments/assets/89f27e6e-5b9f-4055-bcb0-6121bf8f590c" />
<br/>
<br/>
Created separate storage pools for ISO images and virtual machine disk files.
<img width="755" height="527" alt="Pasted image 20260421221726" src="https://github.com/user-attachments/assets/04060af8-7227-4615-b133-ab3557b3239a" />
<br/>
<br/>
Encountered a boot failure while attempting to start the newly created virtual machine.
<img width="1284" height="902" alt="Pasted image 20260420223435" src="https://github.com/user-attachments/assets/b1aef8e0-c8b5-4d21-9f9d-e06fa91f8495" />
<br/>
<br/>
Reviewed VM hardware settings and discovered no installation image was attached to the virtual CD-ROM.
<img width="1284" height="902" alt="Pasted image 20260420223520" src="https://github.com/user-attachments/assets/b51f8e87-b116-4193-8e35-f7f5efaa96be" />
<br/>
<br/>
Attached the Kali Linux ISO and corrected boot settings to prioritize the virtual CD-ROM device.
<img width="1284" height="902" alt="Pasted image 20260420223600" src="https://github.com/user-attachments/assets/46268aba-1a6e-42fc-b364-01c5fcca0bf8" />
<br/>
<img width="1140" height="789" alt="Pasted image 20260421214201" src="https://github.com/user-attachments/assets/b4d668cf-075b-449e-a9e3-4d3fa9295c89" />
<br/>
<br/>
As a result, I Successfully booted, installed, and validated the Kali Linux virtual machine deployment.
<img width="1149" height="1070" alt="Pasted image 20260420231924" src="https://github.com/user-attachments/assets/7fd8594f-f21b-4040-8eec-f36e6a60412e" />

# More Labs
his project provided the foundational infrastructure required for the following labs:

- <b>Enterprise Lab: Windows Server & AD DS Deployment</b>
  - [Enterprise Lab: Windows Server & AD DS Deployment](https://github.com/AllFullPower/Enterprise-Lab-Windows-Server-AD-DS-Deployment)

- <b>Enterprise Help Desk Lab with Active Directory</b>
  - [Enterprise Help Desk Lab with Active Directory](https://github.com/AllFullPower/Ticketing-System-integration-with-AD-Environment)








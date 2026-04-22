# Linux Virtualization Host Setup (QEMU/KVM)

## Objective

## Skills Learned

## Tools Used

# Steps Taken
These are the steps I took to complete this project with some errors that came across included.
<br/>
## Step 1. Creating the partition

Identifying the partition I had to allocate:
<img width="755" height="252" alt="Pasted image 20260407202403" src="https://github.com/user-attachments/assets/d52af78a-011f-45f1-a05f-1b0c4098ca8e" />
<br/>
<br/>
While mounting the partition I had an error:
<img width="721" height="108" alt="Pasted image 20260408203925" src="https://github.com/user-attachments/assets/44199598-688e-46d9-a130-4656529ff2f7" />
<br/>
With a little bit of research I found out that It was because **systemd** has a mental map of the drives on etc/fstab and I had to edit that file before:
<img width="691" height="305" alt="Pasted image 20260421203314" src="https://github.com/user-attachments/assets/c446f6c9-3b4c-41b3-8c6b-d12ce73898e3" />
<br/>
When this file is modified **systemd** still looking for the old version, so my solution was to reload the **systemctl** daemon. After reloading the daemon, it worked:
<img width="721" height="108" alt="Pasted image 20260408211008" src="https://github.com/user-attachments/assets/555cd3c9-d71f-4e38-b330-51d13b5720cd" />
<br/>
<br/>
It was critical to change the ownership of the directory where the new partition is mounted, to prevent future issues:
<img width="721" height="76" alt="Pasted image 20260408213611" src="https://github.com/user-attachments/assets/c26e1b26-7c62-4055-836b-900ff997268b" />

## Step 2. Installing QEMU/KVM and Virtual Machine Manager

First, I checked if virtualization was available on my PC with the next two commands:
- `lscpu | grep virtualization`
- `lsmod | grep kvm_amd`



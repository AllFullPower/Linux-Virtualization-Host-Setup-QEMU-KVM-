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
<br/>
<br/>
## Step 2. Installing QEMU/KVM and Virtual Machine Manager

First, I checked if virtualization was available on my PC with the next two commands:
- `lscpu | grep virtualization`
- `lsmod | grep kvm_amd`
  
<img width="554" height="34" alt="Pasted image 20260410155813" src="https://github.com/user-attachments/assets/5fe174fb-771a-4aa0-ba33-a9e1420fbaad" />
<br/>
<img width="481" height="49" alt="Pasted image 20260410155929" src="https://github.com/user-attachments/assets/d8c3f47a-2809-4066-ab09-799f8408907a" />
<br/>
<br/>
Installing the proper tools:
<img width="825" height="443" alt="Pasted image 20260410162007" src="https://github.com/user-attachments/assets/18979b64-c2f0-4a77-93df-dfd389900284" />
<br/>
<br/>
The needed tools were successfully installed:
<img width="859" height="545" alt="Pasted image 20260410164808" src="https://github.com/user-attachments/assets/5f6121a9-4f67-4e10-83e1-4c5a9d898bb9" />
<br/>
<br/>

## Step 3. Create a Kali VM
> For security reasons, we first checked the checksum of the .iso file we downloaded with the one given by the official website of Kali Linux.
<br/>
<br/>
I created a file with the checksum from the page:
<img width="828" height="72" alt="Pasted image 20260412232528" src="https://github.com/user-attachments/assets/1cbc74f6-4b82-4e34-aaa7-5d6badbec372" />
<br/>
<br/>
Then Checked it against the one generate by the .iso file:
<img width="828" height="72" alt="Pasted image 20260412232800" src="https://github.com/user-attachments/assets/89f27e6e-5b9f-4055-bcb0-6121bf8f590c" />
<br/>
<br/>
I created two storage volumes for different purposes one for images and the other for VMs, and taking advantage of the new partition:
<img width="755" height="527" alt="Pasted image 20260421221726" src="https://github.com/user-attachments/assets/04060af8-7227-4615-b133-ab3557b3239a" />
<br/>
<br/>
I had an error while the VM was booting:
<img width="1284" height="902" alt="Pasted image 20260420223435" src="https://github.com/user-attachments/assets/b1aef8e0-c8b5-4d21-9f9d-e06fa91f8495" />
<br/>
<br/>
I checked the boot order and if the CDROOM had the Kali image, and that's how I found out what was causing the error, there was no image running:
<img width="1284" height="902" alt="Pasted image 20260420223520" src="https://github.com/user-attachments/assets/b51f8e87-b116-4193-8e35-f7f5efaa96be" />
<br/>
<br/>
I solved just by selecting the kali image on the CDROM and then I noticed that in "Boot options" the CDROOM 1 was not checked so I checked that option, that could be causing the problem as well:
<img width="1284" height="902" alt="Pasted image 20260420223600" src="https://github.com/user-attachments/assets/46268aba-1a6e-42fc-b364-01c5fcca0bf8" />
<br/>
<img width="1140" height="789" alt="Pasted image 20260421214201" src="https://github.com/user-attachments/assets/b4d668cf-075b-449e-a9e3-4d3fa9295c89" />
<br/>
<br/>
As a result, I was able to boot the machine, follow the installation process and use my new Kali Linux VM:
<img width="1149" height="1070" alt="Pasted image 20260420231924" src="https://github.com/user-attachments/assets/7fd8594f-f21b-4040-8eec-f36e6a60412e" />










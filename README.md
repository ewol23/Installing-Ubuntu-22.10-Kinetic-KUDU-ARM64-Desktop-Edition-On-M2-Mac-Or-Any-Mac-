# Installing-Ubuntu-22.10-Kinetic-KUDU-ARM64-Desktop-Edition-On-M2-Mac-Or-Any-Mac-
Installing Ubuntu 22.10 Kinetic KUDU ARM64 Desktop Edition On M2 Mac Or Any Mac W/ Apple Silicon. Using UTM
Installing Ubuntu 22.10 Kinetic Kudu ARM64 Desktop Edition on M1 Mac using UTM
In this guide, I'll show you how to install Ubuntu 22.10 on an M1/2 Mac using UTM. UTM is a powerful QEMU emulator that allows you to run Ubuntu inside a virtual machine on any Mac with Apple Silicon. Thanks to Apple's new virtualization framework, you can run ARM64 OS on Apple Silicon at near-native speeds.

Prerequisites
Before you start, ensure you have the following:

An Apple M1 Mac
At least 40 GB of free space on your Mac
A reliable internet connection
Step 1: Download Ubuntu and UTM
Download Ubuntu 22.10 ARM64 ISO file:

Visit the Ubuntu releases page and download the ARM64 version of Ubuntu 22.10.

Download UTM:

Visit the UTM website and download the latest version of UTM for your Mac.

Step 2: Install UTM
Install UTM:

Open Finder and go to the Downloads folder.
Double-click on the UTM.dmg file and drag the UTM icon to the Applications folder.

Open UTM:

Navigate to the Applications folder and open the UTM application.

Step 3: Create a Virtual Machine for Ubuntu
Create a new virtual machine:

Click on the + button to create a new virtual machine.
Choose Virtualize if you are installing ARM64 OS on Apple Silicon for near-native performance.

Configure the VM:

Import the Ubuntu ISO file by selecting Browse and locating the downloaded Ubuntu ISO.
Allocate 4 GB of RAM and set CPU cores to 4.
Do not enable hardware acceleration as it doesn't work well with Ubuntu 22.10.

Allocate storage:

Allocate at least 30 GB of storage space for the virtual machine. It's better to specify more storage space, which will dynamically use your Mac's storage.

Enable file sharing (optional):

Under the Share Directory section, allow any Mac OS folder (e.g., Downloads) to be accessed inside Ubuntu.

Save and start the VM:

Name the virtual machine and click Save.
Tap on the Play button to start the virtual machine.

Step 4: Install Ubuntu
Boot into the Ubuntu installer:

Select Install Ubuntu Server from the boot menu.
Keep in mind that cursor control will be bounded to the guest OS. Press Control + Option to release the cursor back to the host OS.

Complete the installation:

Follow the installer prompts to complete the installation. Use the keyboard shortcuts provided (e.g., up/down arrow keys, Tab, Spacebar, Enter) to navigate the installer.
Set your language, keyboard layout, and create a user account.
Choose the entire virtual disk for installation and complete the partitioning process.

Install additional packages (optional):

Enable the SSH server if you want to connect to the Ubuntu VM from Mac OS.
Choose any additional environments (e.g., Docker) you want to install.

Reboot the VM:

Once the installation is complete, exit the full-screen mode and turn off the virtual machine.

Step 5: Set Up GNOME Desktop
Start the VM:

Start the virtual machine again. This time, it will boot into the Ubuntu server.
Log in with your username and password.

Update the system:

Open the terminal and run:
sh
Copy code
sudo apt update
sudo apt upgrade

Install GNOME desktop:

Run the following command to install the GNOME desktop environment:
sh
Copy code
sudo apt install ubuntu-desktop

Reboot the VM:

Reboot the virtual machine to load the GNOME desktop environment:
sh
Copy code
sudo reboot

Login to GNOME:

Log in to the GNOME desktop environment using your username and password.

Step 6: Enable File Sharing Support
Install VM tools:

Open the terminal and install support for directory sharing between guest OS and host OS:
sh
Copy code
sudo apt install spice-vdagent

Reboot the VM:

Reboot the virtual machine to apply changes.

Enable shared folder:

Open Firefox and type the URL to access the shared directory.
If it doesn't work, use 9pfs (Plan 9 File System) for I/O communication between Ubuntu and Mac OS.
Create a directory in /media named host_shared:
sh
Copy code
sudo mkdir /media/host_shared

Configure 9pfs:

Follow the instructions on the relevant page to enable 9pfs.
Add the following line to /etc/fstab:
sh
Copy code
host_shared  /media/host_shared  9p  trans=virtio,version=9p2000.L,rw  0  0

Set ownership permissions:

Set ownership permissions for the directory:
sh
Copy code
sudo chown -R $USER:$USER /media/host_shared

Access shared folder:

Open the file manager, choose Other Locations from the sidebar, and access the shared folder.

Performance
The performance of Ubuntu inside UTM on an M1 Mac is impressive, with near-native speeds for most applications.
Note that GPU-based acceleration is not fully supported, which may result in choppy animations or transitions, but overall performance is satisfactory.
Deleting the Ubuntu VM
Turn off the virtual machine:

Ensure the VM is turned off.
Delete the VM:

In the UTM main interface, select the virtual machine from the sidebar.
Right-click and choose Delete to remove the Ubuntu VM.

Conclusion
You have successfully installed Ubuntu 22.10 Kinetic Kudu ARM64 Desktop Edition on your M1 Mac using UTM. This method allows you to run Ubuntu in a virtual environment with near-native performance, providing a seamless experience for development or daily use.
Big thanks to KSK Royal for their invaluable guide on installing Ubuntu 22.10 on an M1 Mac using UTM. Consider supporting them at buymeacoffee.com/kskroyal to fuel their continued content creation.

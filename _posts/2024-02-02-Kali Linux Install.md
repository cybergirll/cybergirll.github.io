---
layout: post
title: "Project Kali Install"
subtitle: "Virtualization and Kali Linux"
background: '/img/posts/Kali.jpg'
---

## Background

In the realm of cybersecurity, virtualization plays a crucial role by enabling the creation of isolated virtual environments within a single physical computer. This technology allows for the development of distinct virtual machines, each equipped with its own virtual Central Processing Unit (CPU), Graphics Processing Unit (GPU), Random Access Memory (RAM), Network Interface Card (NIC), storage (HDD, SSD), and input peripherals such as a mouse and keyboard.

The significance of virtualization in cybersecurity lies in its ability to conduct various tasks within these isolated virtual machines, all without compromising the security of the underlying physical machine's operating system. To achieve this, a hypervisor, a specialized software component, must be installed within the host machine's operating system. The hypervisor facilitates hardware virtualization services, ensuring the secure and efficient operation of the virtual environments.

## Setting up your Virtual Environment


![IMDb page](/img/posts/VirtualEnvironment.jpg)


We have outlined instructions for two widely used virtual environments: *VirtualBox* and *Docker*. To initiate the process, opt for either Method #1, which involves configuring VirtualBox and Kali, or Method #2, centered around Docker and Kali.

## Method 1: VirtualBox
#### 1. Download VirtualBox

- Go to **[VirtualBox.org](https://www.virtualbox.org/)**
- Click the big blue button that says "Download VirtualBox".
- Click on the platform package for your operating system.
- Save the file.

#### 2. Install VirtualBox

- Run the installer once the download is finished.
- Select Next to start the installation.
- Select Next to install the default feature set (everything).
- Select Next to choose the default options.
- Select Yes to install the virtual network interfaces. This will allow VirtualBox to create virtual networks and tap into your physical NIC in order for the guest machines to connect to the Internet.
- Select Install.
- Answer `Yes` to the Windows UAC prompt (check for flashing icon in your taskbar)
- Select Finish.

#### 3. VirtualBox Extension Pack

The extension pack will add additional functionality in order to provide a more optimal experience. It will also serve to satisfy a requirement for a later assignment.

*Download the VirtualBox Extension Pack*

- Return to **[VirtualBoxDownloads](https://www.virtualbox.org/wiki/Downloads)**
- Click the link that says *"All supported platforms"* under the Extension Pack section.
- Save the file.

*Install the VirtualBox Extension Pack*

- Open the Extension Pack file you just downloaded.
- Note: It should open in VirtualBox by default, prompting you to Install. If it doesn't then you may need to manually install it by opening VirtualBox, go through the File menu -> Preferences -> Extensions -> Add new package.
- Agree to the terms by bring the scroll bar down and clicking "I Agree".
- Answer `Yes` to the Windows UAC prompt (check for a flashing icon in your taskbar).
- Click `OK` after it successfully installs.

#### 4. Kali Linux Installation

Kali is a Linux distribution (distro) widely utilized by security professionals. It is equipped with over 600 pen testing and forensics tools, and we'll leverage several of these tools. Additionally, Kali will serve as a platform to introduce the Linux command line interface (CLI) to participants who may be unfamiliar with it.

## Initial Setup

#### 1. Download the latest Kali ISO Image

- Go to **[Kali Downloads](https://www.kali.org/downloads/.)**
- Download the image in the first row column. It's 3GB+ and may take a while depending on network speed.

#### 2. Create a new Virtual Machine (VM)

- Open VirtualBox and create a New VM.
- Name it as you wish, set the Type to Linux and Version to Debian, as Kali is a derivative.
- Choose a memory size (powers of 2). We recommend allocating a quarter of your total system memory e.g. if you computer has 8G then set it to 2048 MB. If memory is scarce then stick with 1024 MB. You may be able to get by with less but performance will be heavily impacted due to swapping/paging to disk.
- Create a virtual hard disk, of type VDI, dynamically allocated with AT LEAST 25GB of space. If you have plenty of free space we recommend 50GB.

#### 3. Mounting the ISO and Bootstrapping

- After creating the virtual hard drive you will be back at the main VirtualBox Manager window. From here, make sure the new Kali VM is highlighted blue and click the green arrow Start button.
- Next you'll be prompted for a start-up disk. Click the little folder icon with the green arrow.
- Add a new virtual optical disk image (ISO) file.
- Open the ISO you downloaded previously in your Downloads folder. Then click `Choose.`
- Finally, click Start.

## Kali Installation

#### 1. Configuring the Locale and Hostname

- Once the installer boots up, choose Graphical Install and press `Return/Enter.`
- Next choose your language, location and keyboard layout.
- After a few minutes of loading you will be asked for a hostname. For the purposes of this course you can set this to what you want as long as it is a single lowercase word or you can just leave the default as kali.
- Leave Domain name blank. If you were making the VM a publicly accessible server and linking it to a DNS record, you would use its fully qualified domain name e.g. kali.example.com.

#### 2. Creating a User and Setting a Password

- When setting up your user account, the Full name is your "display" name while the Username for your account is the actual login username. Set your username and password to something you'll remember.
- **WARNING: Usernames in Linux are case-senstive.** When logging in, you must type them exactly as you created them. It may be easier for you (and others) to remember if you follow the standard convention of keeping usernames all lowercase.

#### 3. Timezone, Partitioning, Filesystem layout

- Set your **timezone.**
- Go with the default partition layout of **Guided - use entire disk.**
- Click continue to partition your only virtual disk: **sda.** Note how Linux names its drives. The first SCSI (or SATA) disk attached is named sda. If you attached a second one, it would be named sdb, third would be sdc and so forth.
- Choose **All files in one partition** in order to keep the partitioning layout simple. This will make it easier to enlarge the disk and filesystem later on should the need arise.
- Select **Finish pertaining and write changes to disk** and continue.
- Lastly, confirm **Yes** and continue in order to make the changes take effect. Your final layout has 2 partitions, 1 partition for files and 1 for swap. Swap is used as a sort of RAM backup when the system runs out of memory and needs to write to the hard drive. When a system runs out of RAM it'll bring the system to a crawl. Small amounts of swap space is also used regularly for instance, whenever a low priority process has been asleep for some time and no longer requires high-performance RAM.

#### 4. Software Installation

- Once the base system is installed you'll be asked for proxy information. Leave the field blank (default).
- Next you'll choose which extra software to install. Go with the default Xfce Desktop environment or choose another. GNOME was the default in the last edition of Kali (pre-2020). You can also choose multiple environments to try out, but keep in mind that adding more will use more space on the hard drive. Each one consumes roughly 1G.
- Leave Collection of tools at the default setting and continue.

#### 5. Bootloader Install and Reboot

- Towards the end, you'll be asked to Install the GRUB (GRand Unified Bootloader) to the master boot record (MBR). Mark Yes, continue and choose ```/dev/sda``` to finish the final installation process.

```
Congratulations, the installation is complete! The system will automatically reboot to a login prompt. Sign in.```
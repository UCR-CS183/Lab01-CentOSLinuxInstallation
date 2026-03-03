# Lab01-CentOSLinuxInstallation
## CentOS Linux Installation on VirtualBox or Docker

### Outcomes: 
By the end of this lab, you will know how to:
* Create a virtual machine in VirtualBox.  VirtualBox is a free, cross platform virtualization system, or
* Create a container in Docker. Docker is a free, cross platform containerization system.
* Install the latest version of CentOS 7 Linux in that virtual machine or container (we recommend using the Minimal ISO), and add a user.  CentOS is a widely used free distribution based on Red Hat Enterprise Linux.
* Recover the root password on a CentOS install.  The method of root password recovery varies between distributions, what is most important is that you learn the concept. 
* Minimize which services run at start on your system.  This is an important step for security purposes, and one you will be automating.
* Use and configure 'sudo'.  Sudo allows non-administrative users to run commands with elevated privileges.

#### Rubric: 
Out of 10 points total
* Lab checkoff (2 points): GRUB password & Recover the root password on a CentOS install
* Lab checkoff (5 points): Minimize which services run at start on your system.  -2 points if you do not comment why you are turning off services.
* Lab checkoff (3 points): Use and configure 'sudo'.

#### Turnin
Submit the script that you wrote (with the extension .txt rather than .sh) to turn off services to iLearn, in 'Lab 1', for your lab section.  The checkoff is not valid (you get zero points) without this submission.

### Part 0: To VirtualBox or To Docker
That is the question. Determining whether to use VirtualBox or Docker depends on the environment on your laptop. There are several factors that will help you determine which is the best approach. These factors include what operating system you are running on, and what type of processor your OS is running on.
Windows

If you're running on Windows (hopefully either Windows 10 or Windows 11), you mostly only have one choice, but to run CentOS inside of VirtualBox. Windows 10 and 11 can run Docker, but only if you are running the Pro version of the operating system. Docker requires that the OS support virtualization, which is only possible on the Pro version of Windows. Therefore, you will most likely need to do this lab in VirtualBox.

#### Mac OS X
If you're running on Mac OS X, then you will also need to know what processor you are running on. If you're running on an Intel processor such as i9, i7, i5 or i3, or an AMD processor, then you may choose between either VirtualBox or Docker. If, however, you have a computer with one of the latest Apple silicon, such as the M1 or M2 processor (those are both ARM based processors), your only choice is to run a Docker container. VirtualBox does not currently run on any Apple silicon (or any ARM processor that I know of).

#### Linux
If you're running on Linux, then you will also need to know what processor you are running on. If you're running on an Intel or AMD processor, then you can choose between either VirtualBox or Docker. If, however, you're running these labs on Linux, such as a Raspberry Pi, then you will only be able to run a Docker container. Again, VirtualBox does not currently support any ARM processor that I am aware of.

#### Choosing between VirtualBox and Docker
If you're lucky enough to have a choice between VirtualBox and Docker, the question is, how do you decide which to use. The answer is, it depends. VirtualBox is probably the easiest way. And it's a tool that is used in many real world applications. However, the main drawback is that it uses more resources such as CPU and RAM. It also takes more of your disk space, though not significantly more. Docker on the other hand, is also used in many real world applications, and uses less resources. Sometimes, however, it can be more complex to maintain. It may not appear that way from this lab. The install procedure for Docker is much simpler than for VirtualBox. But that's a one time benefit. Future issues may be harder to solve in Docker.

**Warning.** While it is possible to use both environments, don't let the installation in both environments prevent you from finishing this lab. You are only required to get either VirtualBox or Docker up and running, not both. Be sure to get one of these demoed to the TA and then work on the other once the first environment is working.

### VirtualBox Lab Instructions
If you plan to use Docker rather than VirtualBox, then skip this section and go to the Docker Lab Instructions

#### Part 1: VirtualBox Machine Creation
You are going to create a new Linux virtual machine with 8 GB of disk space and 1024 MB of memory.
Procedure
* Download VirtualBox for your machine from the official websites download page
* Use the download to install the VirtualBox software
* Start VirtualBox and configure the virtual machine as follows:
* The name of the virtual machine should be “Centos”.
* Operating system: Linux
* Version: Red Hat (64 bit)
* Base Memory Size: 1024 MB (should be default)
* You will “Create a virtual hard disk now”
* Use the default VirtualBox Disk Image (VDI) with a size of 8 GB (should be default), choose “Dynamically allocated” for the storage type (should be default).
* On the menu on the left hand side of the screen that appears after you've done the basic setup, look under the 'Network' category on the resulting menu, and verify that "Adapter 1" is set to "NAT".

#### Part 2: CentOS Linux installation
You will install CentOS linux from an iso (DVD) image.

Procedure

* Download the CentOS 7 DVD ISO image from the official websites download page
* Go back to VirtualBox, and double click on 'Storage' (this will bring up the storage management interface); highlight 'Empty', under 'Controller: IDE'.
* Next, look over to the right, on the storage management interface, and you should see a section titled 'Attributes'. Click on the icon next to the 'CD/DVD Drive' section, and add the iso mentioned in 1 from the drop down menu, "Choose a virtual CD/DVD disk file".
* Choose the CentOS 7 DVD ISO that you downloaded previously and hit “ok”
* Start the virtual machine. It will boot off of the ISO image that you specified.
* Select "Install CentOS 7" from the boot menu.
* Follow instructions.  The critical non-default steps are listed here in the order you will encounter them:
* If your installation starts to perform a media test, hit “esc” to skip it. It is irrelevant because we are not using physical media
* Say “yes” if warned about erasing all data.
* Perform the following steps in the CentOS 7 Installation Screen:
    - In the Date & Time menu change the city from the default “New York” to “Los Angeles”
    - In the Software Selection menu make sure that “Minimal Install” is selected. This will install the OS without the GUI which is typical for servers
    - In the Network & Host Name section set the host name to your CS login.
    - Also click on "Configure Network", select the only available network connection (it should be enp0s3), select "Edit" and then select "Automatically connect to this network when it is available"
        - If no network interface is shown during this step of the installation then you can modify the /etc/sysconfig/network-scripts/ifcfg-enp0s3 file to have ONBOOT=yes. Restart the server after making this change for it to take effect.
    - When asked which type of installation you would like, select "Create Custom Layout"
    - In the installation destination section choose “I will configure partitioning”
* Once the installation starts, set a root password. Make sure to choose a good and strong password!
* Once the install has finished, reboot the system. You may see that the system attempts to boot off the CD again. If this is the case, close the window for the VM, by going to “Machine”->”Close” selecting “Power off ”, and go into the “System” settings, and remove the disk from the virtual CD drive.
* Login as root using the username root and the password you set during installation
* Turn off SELinux by editing /etc/selinux/config. If you are not familiar with vi, you can use another text editor such as nano or emacs. Change the line in the file 'SELINUX=enforcing' to 'SELINUX=disabled'.
* Update all packages by running 'yum update'.  This is important to ensure that the OS is up to date.
* Reboot.
* Create an account for yourself using 'useradd'. 'man useradd' for options if you want to do something other than the default. You will need to set up a password for the account using the 'passwd' command.  Make sure that the new account has the same username as your CS account.
* Log in with the account to make sure it works.
* **Note:** Once installation is complete, using VirtualBox, take a snapshot of the virtual machine to provide the ability to roll back to a clean installation.

### Part 3: Setting a GRUB Bootloader Password
Once you have installed CentOS you will need to add a password to your bootloader. Because the bootloader will allow you to log into secured portions of the kernel to perform rescue operations or to boot to other kernels which may not respect any permissions you have set, it is as important (if not more important) to secure as your root account.

Follow this tutorial (https://www.myrandomtips.com/linux/centos7/set-grub-password-centos7/) to create a bootloader password hash and add that to the GRUB configuration files. Make sure to remember this bootloader password as you’ll need it for the next step. Note that because you don’t have access to your mouse on your minimal server installation you will need to use output redirection to save the output hash to use in the GRUB configuration file.

After you have set the bootloader password, reset your machine and verify that going into the GRUB editor for one of the kernels (with ‘e’ at the GRUB menu) now requires a password. 

**Checkoff:** Once you have verified that the bootloader now requires a password, reboot your machine again and demo this to your TA.

### Part 4: Root password recovery
Now that you have secured your GRUB with a bootloader password, you should follow these directions (https://www.unixmen.com/reset-root-password-centos-7/) to reset your root password by logging into the kernel in single user mode.

Separate from this lab and as an exercise for the reader, what  could you do if you forgot the bootloader password as well? 

### Part 5: Determine what services run at boot time
Here are general background resources about how to determine which services are running that may be useful:
* A walkthrough on how to use systemctl on CentOS 7 to modify the system's boot services. https://www.theurbanpenguin.com/managing-linux-services/
* Some recommendations for services to leave alone or kill. Note that this is neither definitive nor authoritative. Some services may exist on a server that are not listed, and depending on use case some services may need to be left running where this guide recommends disabling them. You still need to make justifications based on your use case. https://www.cyberciti.biz/faq/linux-default-services-which-are-enabled-at-boot/ 

**Checkoff:** show the TA the status of your boot services currently running by executing the appropriate systemd command to list services and answering any questions about the purpose of a service such as sshd.

### Part 6: Add an ordinary user to restart the network service
Use 'sudo' and the sudoer file to provide the user you created above the ability to restart the 'network' service, but no other sudo privileges. You should see the network service still active in the list of services above in the previous topic. Use any available resources – man pages, the book, internet research, configuration files on the server itself, in order to do this. 

**Hint:** It requires adding one line of configuration to one file. Once you have this set up, demo it to the TA.

**Checkoff:** Restart the network service as your new user. Show that the user can not perform other sudoer actions, e.g. ‘sudo cat /etc/shadow/‘

### Part 7: VirtualBox to Host Sharing
In order to create a shared folder that will allow you to easily transfer files between your VirtualBox and your host machine, please follow these instructions.

### Part 8: Snapshotting the current state of your virtual machine
It is probably a good habit to develop to take a snapshot of all changes to your virtual machine during and definitely as you complete each lab. The main benefit to this habit is that if you make mistakes, you can always go back to the last snapshot.

To take a snapshot of your virtual machine, in the Oracle VM VirtualBox Manage click on your virtual machine and click on the hamburger icon to the right of the VM name and select Snapshots. Next, click on the Take icon at the top. Fill in the Snapshot Name. Give it a meaningful name such as CS183 Lab 1. In the Snapshot Description, describe the current state of the virtual machine. The more information you give, the more likely you are to be able to go back to the snapshot you need if issues are discovered in future labs.

Continue to take these snapshots at the end of each lab.

## Docker Lab Instructions

### Part 1: Docker Container Creation
You are going to create a new CentOS 7 Docker Container.
Procedure
* Install Docker for your machine. For Windows and Mac OS X, install Docker Desktop  as described on the official Docker website. You can install Docker Desktop for Linux, if instructions for your Linux distribution are not listed below. For Linux, follow these instructions for your specific distribution.
    - For Ubuntu or Debian use these directions. Follow the directions in the "Install Docker Engine" section. You should only need to do steps 1 and 3.
    - For Centos use these directions. Follow the directions in the "Install Docker Engine" section. You should only need to do steps 1, 3 and 4.
    - For Fedora use these directions. Follow the directions in the "Install Docker Engine" section. You should only need to do steps 1, 3 and 4.
* Create a directory on your computer for this installation
* Create the necessary ssh keys of type RSA, ED25519 and ECDSA for your host platform
    - On windows, install ssh-keygen using these directions.
    - On Mac OS X, ssh-keygen should already be installed.
    - On Linux, ssh-keygen should already be installed.
    - Once ssh-keygen is installed execute the following in a terminal window:
```sh
$ ssh-keygen -t rsa -N '' -f ./ssh_host_rsa_key
$ ssh-keygen -t ed25519 -N '' -f ./ssh_host_ed25519_key
$ ssh-keygen -t ecdsa -N '' -f ./ssh_host_ecdsa_key
```

* In this directory create a Dockerfile and put the following text in it:
```dockerfile
FROM centos:7
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]


RUN yum update -y 
RUN yum --setopt=tsflags='' -y install man man-pages man-db
RUN yum --setopt=tsflags='' -y install openssh openssh-server 
RUN yum --setopt=tsflags='' -y install openssh-clients sudo 
RUN yum --setopt=tsflags='' -y install initscripts


# Generate keys
COPY ssh_host_rsa_key /etc/ssh/ssh_host_rsa_key
RUN chmod 600 /etc/ssh/ssh_host_rsa_key
COPY ssh_host_ed25519_key /etc/ssh/ssh_host_ed25519_key
RUN chmod 600 /etc/ssh/ssh_host_ed25519_key
COPY ssh_host_ecdsa_key /etc/ssh/ssh_host_ecdsa_key
RUN chmod 600 /etc/ssh/ssh_host_ecdsa_key


RUN adduser <choose a username>
RUN echo <username above>:<choose a password> | chpasswd
RUN usermod -aG wheel <username above>


EXPOSE 22


CMD ["/usr/sbin/init"]
```

* Build and tag the image with the following command in a terminal window:
```sh
$ docker build . --tag local/cs183-centos-systemd
```


* We will use the Docker compose plugin to start and stop the image. Create the file docker-compose.yml in the same directory as your Dockerfile and put the following text in it:
```yaml
version: '3.9'
services:
 cs183-main:
   image: local/cs183-centos-systemd
   build: .
   privileged: true
   hostname: cs183-<username above>-main
   ports:
     - '2020:22'
   volumes:
     - type: bind
       source: "${HOME}/cs183"
       target: /home/<username above>/cs183
     - '/sys/fs/cgroup:/sys/fs/cgroup:ro'
```


* To start the container using the image built in the previous step, execute the following command in a terminal window:
```sh
$ docker compose up -d
```

* Now you can login to this container using SSH on port 2020. For most systems you can use the following command:
```sh
$ ssh <username above>@localhost -p 2020
```

* When you're done exploring your container, type 'exit' to leave the SSH session. To stop the container, execute the following command in a terminal window:
```sh
$ docker compose down
```

### Part 2: Determine what services run at boot time
Here are general background resources about how to determine which services are running that may be useful:
* A walkthrough on how to use systemctl on CentOS 7 to modify the system's boot services. https://www.theurbanpenguin.com/managing-linux-services/
* Some recommendations for services to leave alone or kill. Note that this is neither definitive nor authoritative. Some services may exist on a server that are not listed, and depending on use case some services may need to be left running where this guide recommends disabling them. You still need to make justifications based on your use case. https://www.cyberciti.biz/faq/linux-default-services-which-are-enabled-at-boot/ 

**Checkoff:** show the TA the status of your boot services currently running by executing the appropriate systemd command to list services and answering any questions about the purpose of a service such as sshd.

### Part 3: Add an ordinary user to restart the network service
Make sure your docker container is up and running and then SSH into it. Then, use 'sudo' and the sudoer file to provide the user you created above the ability to restart the 'network' service, but no other sudo privileges. You should see the network service still active in the list of services above in the previous topic. Use any available resources – man pages, the book, internet research, configuration files on the server itself, in order to do this. 

**Hint:** It requires adding one line of configuration to one file. Once you have this set up, demo it to the TA.

**Checkoff:** Restart the network service as your new user. Show that the user can not perform other sudoer actions, e.g. ‘sudo cat /etc/shadow/‘

### Part 4: Committing changes to your container
In future labs, and perhaps even this lab, you will change the configuration for a container and you may need to bring the container down between labs. The problem is, when you stop a container those changes will be lost. Rather than having to add these changes to the Dockerfile, Docker allows you to commit these changes to any running container after the necessary changes have been made. It is probably a good habit to develop to commit all changes to your container during and definitely as you complete each lab. The other benefit to this habit is that if you make mistakes, you can always go back to the last commit.


To commit a currently running container, you must first determine its ID. To find the IDs for all the currently running containers, run the following command in the terminal on the host machine:

```sh
$ docker ps
CONTAINER ID   IMAGE        COMMAND   CREATED     STATUS      PORTS  NAMES
d15a7e7c08a2   4e7c84fe4df4 /bin/bash 22 days ago Up 22 hours        labs-cs183-main-1
```

With the Container ID you can now commit the changes by running the following command in the terminal on the host machine:

```sh
$ docker commit d15a7e7c08a2 local/cs183-centos-systemd:lab-1
```

This command will temporarily pause the running container, snapshot all the new configuration and update the tag. The lab-1 at the end of the tag name allows you to tag each lab individually, allowing you to go back to whatever configuration you need.

Be sure to execute the command and commit your work from this lab in preparation for the next lab.

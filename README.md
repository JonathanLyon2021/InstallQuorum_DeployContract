# InstallQuorum_DeployContract
This is Exercise 19 from MI4 in Kingsland Universities Blockchain Developer Program.

# Overview
The goal of this exercise is to install and setup **Quorum**. Quorum is a **permissioned blockchain software** based on
Ethereum. This is ideal for private entities and enterprise cases that want some kind of user-access control for the
blockchain network. This open-source development effort is headed by J.P. Morgan and Microsoft.

# Goals
• Bring a Quorum node and multiple nodes online via Virtual Box and Vagrant.
• Interact with the Quorum nodes on the virtual machine using Quorum samples.

# Prerequisites
• GIT v2.26.0^ https://git-scm.com/downloads
• Virtual Box v6.1.2 https://www.virtualbox.org/wiki/Download_Old_Builds_6_1
• Vagrant v2.2.7 https://releases.hashicorp.com/vagrant/2.2.7/
You may find that the instructions are primarily directed for Windows OS, if you are using other operating systems,
the instructions should still be relatively similar especially on installation of required exercise dependencies. Do not
hesitate to reach out to the course platform if you are encountering any issues.

## 1. Install VirtualBox
1. We will use VirtualBox to create an instance of the private blockchain. Download VirtualBox from here
https://www.virtualbox.org/wiki/Download_Old_Builds_6_1 and choose the version of your OS.
2. Run the installer wizard and press next.

3. Press next on the Custom Setup tab.

4. Choose the options that you want for your VirtualBox setup.

5. Accept any succeeding prompts to continue with the installation.

## 2. Install Vagrant
1. Go to https://releases.hashicorp.com/vagrant/2.2.7/ and download Vagrant for your OS.
If you encounter this after clicking on the installer file, click **More Info** and **Run Anyway:**

2. Run the installer and press [next]

3. Accept the terms and conditions and press [next]

4. Select the preferred installation directory:

5. Accept any succeeding prompts to continue with the installation.
6. Restart your computer to complete the installation.

## 3. Install Quorum, Run Your Own Blockchain, and Deploy a Contract
1. Before we proceed to launch Quorum, we need to clone the quorum-examples repository.
Navigate to your preferred directory and launch a terminal on that location. Then, run this command:

    git clone https://github.com/jpmorganchase/quorum-examples

2. Navigate to the quorum-examples directory on the terminal.

    cd quorum-examples

3. Now, start a Vagrant instance in the folder.
vagrant up

4. During this process, Vagrant will make an Ubuntu instance in your virtual machine and download all that is
necessary for Quorum. This will take a while, go grab that coffee and take a break.
When Quorum is ready, you’ll see this:

5. Now we have a virtual machine with everything needed to build Quorum network and you can access it with:
vagrant ssh

6. Now, go to the **quorum-example/7nodes.**

    cd quorum-examples/7nodes
7. Then, to add the consensus mechanism, we will use **raft** for this exercise.
8. The following command will initialize the **raft** consensus.

    ./raft-init.sh

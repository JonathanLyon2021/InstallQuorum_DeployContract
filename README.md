# InstallQuorum_DeployContract
This is Exercise 19 from MI4 in Kingsland Universities Blockchain Developer Program. This whole program is run completely using command prompts, sometimes 2 or 3 of them at a time.

# Overview
The goal of this exercise is to install and setup **Quorum**. Quorum is a **permissioned blockchain software** based on
Ethereum. This is ideal for private entities and enterprise cases that want some kind of user-access control for the
blockchain network. This open-source development effort is headed by J.P. Morgan and Microsoft.

# Goals
• Bring a Quorum node and multiple nodes online via Virtual Box and Vagrant.
• Interact with the Quorum nodes on the virtual machine using Quorum samples.

# Prerequisites
• GIT v2.26.0^ *https://git-scm.com/downloads*
• Virtual Box v6.1.2 https://www.virtualbox.org/wiki/Download_Old_Builds_6_1
• Vagrant v2.2.7 *https://releases.hashicorp.com/vagrant/2.2.7/*
You may find that the instructions are primarily directed for Windows OS, if you are using other operating systems,
the instructions should still be relatively similar especially on installation of required exercise dependencies. Do not
hesitate to reach out to the course platform if you are encountering any issues.

## 1. Install VirtualBox
1. We will use VirtualBox to create an instance of the private blockchain. Download VirtualBox from here
*https://www.virtualbox.org/wiki/Download_Old_Builds_6_1* and choose the version of your OS.
2. Run the installer wizard and press next.

3. Press next on the Custom Setup tab.

4. Choose the options that you want for your VirtualBox setup.

5. Accept any succeeding prompts to continue with the installation.

## 2. Install Vagrant
1. Go to *https://releases.hashicorp.com/vagrant/2.2.7/* and download Vagrant for your OS.
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
When Quorum is ready, you'll see a QUORUM written out in "/"'s on the command prompt.

5. Now we have a virtual machine with everything needed to build Quorum network and you can access it with:
vagrant ssh

6. Now, go to the **quorum-example/7nodes.**

    cd quorum-examples/7nodes
7. Then, to add the consensus mechanism, we will use **raft** for this exercise.
 The following command will initialize the **raft** consensus.

    ./raft-init.sh
    
8. After successful initialization, start the raft consensus and start the nodes:

        ./raft-start.sh
You might see some repeated messages like: Waiting until all Tessera nodes are running...
This is normal. 

Now, seven nodes are running in the network.

9. Deploy a pre-defined contract with this script:

        ./runscript.sh private-contract.js
The output will be the transaction hash from the interaction.

Take note of the transaction hash, you will need it later.
Run the first node with:

        geth attach qdata/dd1/geth.ipc
An interactive Javascript terminal will start.

10. Check the transaction details by providing the transaction hash.
        
        web3.eth.getTransactionReceipt(‘YOUR_TRANSACTION_HASH’)

*Take note of the contract address, you’ll need it later.*
Awesome. You have successfully deployed a contract on the private blockchain!

## 4. Interacting with the Deployed Contract
1. Open 2 more separate terminals to run the different nodes. Navigate to your Quorum folder workspace and
run Vagrant just like what you did on the previous exercise. As a review, you would have issued the
following commands:

        cd YOUR_WORKSPACE_FOLDER/quorum-examples
        vagrant ssh
        cd quorum-examples/7nodes

In terminal 2, run node 2:

        geth attach ipc:qdata/dd2/geth.ipc
In terminal 3, run node 7:

        geth attach ipc:qdata/dd7/geth.ipc

2. After that, in each terminal, including the previous terminal 1, define the contract:

        var contractAddress = "YOUR_CONTRACT_ADDRESS"
        var abi =
        [{"constant":true,"inputs":[],"name":"storedData","outputs":[{"name":"","type":"uint
        256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"x","t
        ype":"uint256"}],"name":"set","outputs":[],"payable":false,"type":"function"},{"cons
        tant":true,"inputs":[],"name":"get","outputs":[{"name":"retVal","type":"uint256"}],"
        payable":false,"type":"function"},{"inputs":[{"name":"initVal","type":"uint256"}],"t
        ype":"constructor"}];
        var contract = eth.contract(abi).at(contractAddress)
        
Looking good so far? Awesome!

3. Now go to terminal 1 and call the get() method of the contract.

        contract.get()
The output will be 42.

4. Interact with the contract by calling the **set()** function. Use the **first** terminal.
To make things more interesting, use the **privateFor** option to make a private transaction that only the **first**
and **seventh** node can see.
ROAZBWtSacxXQrOe3FGAqJDyJjFePR5ce4TSIzmJ0Bc= is derived from the public key of the **seventh** node. It can
be found in **quorum-examples/7nodes/keys/tm7.pub**
        
        contract.set(1234,{from:eth.coinbase,privateFor:["ROAZBWtSacxXQrOe3FGAqJDyJjFePR5ce4TSIzmJ0Bc="]});

After the **set()** interaction, run **contract.get()** on each terminal:
The **first** terminal the output will be.

        Output : 1234
If you open the second terminal, the output will be zero, because the data is hidden for him:

        Output : 0
If you open the third terminal where we allow access to the transaction, you will see the number that we expect.

        Output : 1234
        
### Congratulations! You've completed the exercise!

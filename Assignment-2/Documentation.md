# Vagrant Environment Setup Script Documentation

This script is designed to create a Vagrant environment with two virtual machines, a master node, and a slave node. The master node serves as a load balancer, and the slave node acts as a web server. This documentation explains the steps and procedures for executing the script.

## Pre-requisites

Before executing the script, ensure that you have the following pre-requisites installed on your system:

1. [Vagrant](https://www.vagrantup.com/)
2. [VirtualBox](https://www.virtualbox.org/)

## Run the Script

#### Make the script executable
```bash
chmod u+x Vagrant_LAMP.sh
```

#### Run the script
```bash
./Vagrant_LAMP.sh
```

## Execution Steps and Procedures

### Step 1: Create a Shared Folder

The script starts by creating a shared folder named "shared_folder" to facilitate data exchange between the host and virtual machines.

### Step 2: Define Vagrant Configuration

The script uses Vagrant to define the configuration of the virtual machines. It specifies settings for the virtual machines, including their base box, network configurations, and provisioning scripts.

### Step 3: Master Node Configuration

The script configures the master node as follows:

- Hostname: "master-node"
- Private IP Address: "192.168.33.10"
- VirtualBox Configuration: 2GB RAM and 2 CPUs

### Step 4: Provisioning for Master Node

The provisioning script for the master node performs several tasks, including:

- Updating the package list using `apt-get`.
- Creating a user named ``altschool`` with the password ``12345`` and granting it sudo privileges.
- Generating an SSH key for the ``altschool`` user and copying the public key to the shared folder.
- Creating a directory at `/mnt/altschool` and a sample text file within it.
- Installing Apache, MySQL, PHP, and other required packages.
- Starting and enabling the Apache and MySQL services.
- Creating a PHP test file in the web server directory.
- Installing and configuring Nginx as a load balancer and configuring a default HTML page.

### Step 5: Slave Node Configuration

The script configures the slave node as follows:

- Hostname: "slave-node"
- Private IP Address: "192.168.33.11"
- VirtualBox Configuration: 2GB RAM and 2 CPUs

### Step 6: Provisioning for Slave Node

The provisioning script for the slave node includes:

- Updating the package list using `apt-get`.
- Copying the public key from the shared folder (copied by the master node) to the `authorized_keys` file for the "vagrant" user, allowing SSH access.
- Creating a directory at `/mnt/altschool/slave` and copying the contents from the shared folder to this location.
- Installing Apache, MySQL, PHP, and other required packages.
- Starting and enabling the Apache and MySQL services.
- Creating a PHP test file in the web server directory.

### Step 7: Create the Vagrant Environment

After defining the configurations and provisioning scripts, the script concludes with starting the Vagrant environment by executing the `vagrant up` command. This command will create, configure, and provision the virtual machines based on the defined settings.

### Step 8: Access and Testing

Once the Vagrant environment is up and running, you can access the master node and slave node via SSH using `vagrant ssh master` and `vagrant ssh slave`. You can test the configuration, the load balancing, and the web server functionality as per your requirements.

![Apache](assets/Apache%20Confirmation.png)

![Vagrant](assets/Vagrant%20Master-Slave%20Confirmation.png)




**Note:**

- Make sure that you have an active internet connection when executing the script as it requires downloading the base box image for the virtual machines.
- The script sets some sensitive passwords (e.g., MySQL root password) to ``12345`` for demonstration purposes. In a production environment, alpha-numeric password combinitaion should be utilized to comply with security standards for strong and secure passwords.
- Ensure that Vagrant and VirtualBox are installed and properly configured on your system before executing the script.
- If you run into problems with the configuration ``e.g. Vagrant ssh``, especially if you use Vagrant on a windows machine, Kindly utilize ``wsl`` to configure the virtual machine using Vagrant. You can follow the below steps to configure ``wsl`` for your machine.





# Optional

## Running Vagrant with VirtualBox on WSL 2

To run Vagrant with VirtualBox on WSL 2, follow these steps:

1. **Install Windows Subsystem for Linux (WSL) 2**

    Ensure that you have WSL 2 installed on your Windows machine. You can follow Microsoft's official documentation [here](https://docs.microsoft.com/en-us/windows/wsl/install-wsl2).

2. **Install a Linux Distribution**

    Install a Linux distribution of your choice from the Microsoft Store. Ubuntu is a popular choice.

3. **Set WSL 2 as Default**

    Make sure WSL 2 is set as your default WSL version by running the following command in PowerShell with administrative privileges:

    ```Powershell
    wsl --set-default-version 2
    ```

4. **Install VirtualBox on Windows**

    Download and install Oracle VirtualBox for Windows from the [official website](https://www.virtualbox.org/wiki/Downloads).

5. **Install Vagrant on Windows**

    Download and install Vagrant for Windows from the [official website](https://www.vagrantup.com/downloads).

6. **Configure WSL 2 to Use VirtualBox**

    By default, WSL 2 uses Hyper-V for virtualization. To switch to VirtualBox, you need to create a configuration file for WSL 2. Create or edit the `etc/wsl.conf` file in your Linux distribution with the following content:

    ```powershell
    [wsl2]
    kernel=C:\\Users\\<YourUsername>\\vmlinux
    ```
    
    Replace `<YourUsername>` with your actual Windows username.

7. **Download a Vagrant Box**

    Use the `vagrant box add` command in your Linux distribution to download a base box for your virtual machine. For example:
    
    ```bash
    vagrant box add ubuntu/bionic64
    ```
    

8. **Create and Provision Your Vagrant Environment**

    Navigate to your project directory, create a `Vagrantfile`, and configure it according to your needs. You can specify the provider (VirtualBox) and customize your virtual machine settings in this file.

9. **Start Your Vagrant Environment**

    Run the following command in your project directory to start your Vagrant environment:

    ```bash
    vagrant up --provider=virtualbox
    ```
    

10. **SSH into Your Vagrant Box**

    Once your Vagrant environment is up and running, you can SSH into it using the following command:

    ```bash
    vagrant ssh
    ```
    
Now, you should have Vagrant running with VirtualBox on WSL 2. You can manage your virtual machines as usual using Vagrant commands within your Linux distribution in WSL 2.
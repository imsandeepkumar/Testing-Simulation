# Testing-Simulation
A vulnerable machine for pentesting is a system with weakened security for learning and testing cybersecurity skills. It simulates real-world vulnerabilities like outdated software and misconfigurations, allowing users to practice attacks safely. Multiple users can interact with their own instances, ideal for training and collaborative learning.



step 1: Create the NAT Network
1. **Open VirtualBox**.
2. Go to **File > Host Network Manager**.
3. Click on the **NAT Networks** tab.
4. Click **Create** (if no NAT network exists), or edit an existing NAT network.
5. Modify the settings:
   - Set the network range to `10.0.2.0/24` by clicking the **Network CIDR** field and typing `10.0.2.0/24`.
   - Set the **Network Name** for future reference (e.g., `NATNetwork1`).

Step 2: Configure the Virtual Machine's Network
1. Select the virtual machine you want to configure and click **Settings**.
2. Navigate to **Network**.
3. Under **Adapter 1** (or any other available adapter), do the following:
   - **Enable Network Adapter**: Ensure this checkbox is checked.
   - **Attached to**: Select **NAT Network** from the dropdown menu.
   - **Name**: Choose the NAT Network you just created (e.g., `NATNetwork1`).

 Step 3: Configure Static IP Address
To ensure the machine gets the static IP address `10.0.2.15`, you need to configure it manually within the virtual machine.


 For Linux:
1. Boot up your virtual machine.
2. Open a terminal and find the network interface name using:
  
   ip a

3. Edit the network configuration file (usually located in `/etc/netplan/` or `/etc/network/interfaces`, depending on your distribution).

   For Ubuntu (Netplan configuration):
   Open the configuration file:
 
     sudo nano /etc/netplan/00-installer-config.yaml

   - Add the static IP configuration:
   
     network:
       ethernets:
         <interface-name>:
           dhcp4: false
           addresses: [10.0.2.15/24]
           gateway4: 10.0.2.1
           nameservers:
             addresses: [8.8.8.8, 8.8.4.4]
       version: 2

   Replace `<interface-name>` with your actual network interface name (e.g., `enp0s3`).
   

   sudo netplan apply


For Windows:
1. Boot your virtual machine and log in.
2. Open **Control Panel > Network and Sharing Center > Change Adapter Settings**.
3. Right-click your network adapter (likely called `Ethernet` or `Local Area Connection`) and choose **Properties**.
4. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
5. Select **Use the following IP address**, and enter the following:
   - **IP address**: `10.0.2.15`
   - **Subnet mask**: `255.255.255.0`
   - **Default gateway**: `10.0.2.1`
6. Set the **DNS server** to `8.8.8.8` (Google DNS) or any other preferred DNS server.
7. Click **OK** and then **Close**.

 Step 4: Test the Configuration
1. Restart your virtual machine.
2. Once booted, verify the IP address by running:
   - Linux: `ip a`
   - Windows `ipconfig`
   
   You should see `10.0.2.15` assigned to your virtual machine.

3. Test network connectivity by pinging an external server (e.g., `ping google.com`).
****

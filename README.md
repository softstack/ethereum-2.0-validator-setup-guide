# How to setup a fast and secure Ethereum 2.0 validator node with OVHcloud

https://img.shields.io/twitter/url?url=https%3A%2F%2Fgithub.com%2Fchainsulting%2Fethereum-2.0-validator-setup-guide

## Introduction

Ethereum 2.0 is the next step in the evolution of Ethereum. It brings with it many changes, including Proof-of-Stake, Sharding, new client implementations, new cryptography and more.

## Be a validator
* have learned the essentials by watching ['Intro to Eth2 & Staking for Beginners' by Superphiz](https://www.youtube.com/watch?v=tpkpW031RCI)
* have passed or is actively enrolled in the [Eth2 Study Master course](https://ethereumstudymaster.com)
* and have read the [8 Things Every Eth2 validator should know.](https://medium.com/chainsafe-systems/8-things-every-eth2-validator-should-know-before-staking-94df41701487)

## 1.	Prerequisites

### 1.1 Recommended Hardware Setup
* **Operating system:** 64-bit Linux (i.e. Ubuntu 20.04 LTS Server or Desktop)
* **Processor:** Quad core CPU, Intel Core i7–4770 (3,40 GHz / Cores: 4 Threads: 8) or AMD FX-8310 or better
* **Memory:** 16GB DDR4 RAM or more
* **Storage:** 2TB NVMe or more, IOPS: 10,000 (medium speed) and 16,000 (fast)
* **Internet:** Broadband internet connections with speeds at least 10 Mbps without data limit.
* **Power:** Reliable electrical power with uninterruptible power supply (UPS)
* **ETH balance:** at least 32 ETH and some ETH for deposit transaction fees
* **Wallet:** Metamask installed

### 1.2 Self-hosting vs. Dedicated Server by OVH

Having your own hardware
First solution, buy equipment optimized for our needs and run it at home.

| :white_check_mark: Benefits  | :x: Disadvantages |
| ------------- | ------------- |
| Cost optimization | Electricity and internet suppliers reliability  |
| Possibility of reselling the equipment | Price of electricity |
| Optimal participation to decentralization | Equipment maintenance  |
| Physical security | Risk of having unsuitable equipment  |

Using a dedicated server

| :white_check_mark: Benefits  | :x: Disadvantages |
| ------------- | ------------- |
| Electrical, network, and hardware security  | Premium to pay  |
| Upgradability | Money invested is wasted |
| No additional cost on your electricity bill | Less decentralization but mostly 99% up-time  |
| Physical security | Risk of having unsuitable equipment  |

Regarding physical security: https://docs.ovh.com/gb/en/dedicated/securing-a-dedicated-server/

### 1.3 Buy a dedicated server

Go to https://www.ovhcloud.com/en/bare-metal/prices/

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190447406-dbb77299-1632-4c54-a223-3e3b655ee025.png">

**Compare** <br>

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190447790-cf0b5d81-8ecb-4513-b1c8-b65549ed58ca.png">

Advance-1 gen2 for fast sync and Rise-1 for medium sync speed, you can decide 

We have chosen Advance-1 Gen2 with 1Gbit/s unmetered, guaranteed traffic and enough disk space to keep up with the chain increase for a while. 

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190448972-0b325283-0cdb-4795-8599-3099db19aab2.png">

Rent for 24 months and pay all upfront to earn in total 15% discount + free setup fee

<img width="249" alt="image" src="https://user-images.githubusercontent.com/33572557/190449264-27ef97b5-c31a-452a-ad63-199e9039d4d4.png">

It will take around 24h until the dedicated server is ready for setup

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190449918-da7debac-4886-4081-ae1b-f59701a11cfb.png">

### 1.4 Initial Setup
Once you got an email regarding the successful creation of the server, go to your dedicated server dashboard and start the initial setup.<br>
**Go to:** https://www.ovh.com/manager/#/dedicated/server/.. 

<img width="450" alt="image" src="https://user-images.githubusercontent.com/33572557/190451473-a0326871-81a1-4eef-a076-da0c4b5e1a3c.png">

Install the preferred OS, via “Last operating system (OS) installed by OVHcloud” 

> **Note**
> Creating a server requires you to add an SSH Key, follow the guide 
> https://docs.ovh.com/gb/en/dedicated/creating-ssh-keys-dedicated/ 


We recommend **Ubuntu Server 20.04 LTS "Focal Fossa" - ubuntu2004-server 64 bit.** 
In the last step you must set the SSH key and host name, before you are able to install the OS.

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190453011-fb3bcebb-0871-4156-b95a-b92995611a79.png">

## 2. Hardening you node

### 2.1 Login via SSH to your server. Run the following command:
```
ssh ubuntu@162.19.19.1
```
### 2.2 Create a non-root user with sudo privileges. Run the following commands:
```
sudo useradd -m -s /bin/bash ethereum
```
Set the password for ethereum user
```
sudo passwd ethereum
```
Add ethereum to the sudo group
```
sudo usermod -aG sudo ethereum
```
### 2.3 Disable SSH password Authentication and Use SSH Keys only

The basic rules of hardening SSH are:

* No password for SSH access (use private key)
*	Don't allow root to SSH (the appropriate users should SSH in, then su or sudo)
*	Use sudo for users so commands are logged
*	Log unauthorized login attempts (and consider software to block/ban users who try to access your server too many times, like fail2ban)
*	Lock down SSH to only the ip range your require (if you feel like it)

Transfer the public key to your remote node. Update keyname.pub appropriately.
```
ssh-copy-id -i $HOME/.ssh/keyname.pub ethereum@server.public.ip.address
```

Login with your new ethereum user
```
ssh ethereum@server.public.ip.address
```

Disable root login and password based login. Edit the /etc/ssh/sshd_config file
```
sudo nano /etc/ssh/sshd_config
```
```
Locate ChallengeResponseAuthentication and update to no
ChallengeResponseAuthentication no

Locate PasswordAuthentication update to no
PasswordAuthentication no

Locate PermitRootLogin and update to prohibit-password
PermitRootLogin prohibit-password

Locate PermitEmptyPasswords and update to no
PermitEmptyPasswords no

Locate Port and customize it your random port.
Use a random port # from 1024 thru 49141. Check for possible conflicts.

Port <port number>
```

Validate the syntax of your new SSH configuration.
```
sudo sshd -t
```

If no errors with the syntax validation, restart the SSH process
```
sudo systemctl restart sshd
```

Verify the login still works and login with ssh
```
ssh ethereum@server.public.ip.address -p <custom port number>
```

### 2.4 Update your system

It's critically important to keep your system up-to-date with the latest patches to prevent intruders from accessing your system.
```
sudo apt-get update -y && sudo apt dist-upgrade -y
sudo apt-get autoremove
sudo apt-get autoclean
```

Enable automatic updates so you don't have to manually install them.
```
sudo apt-get install unattended-upgrades 
sudo dpkg-reconfigure -plow unattended-upgrades
```

### 2.5	Disable root account

System admins should not frequently log in as root in order to maintain server security. Instead, you can use sudo execute that require low-level privileges.

```
# To disable the root account, simply use the -l option.
sudo passwd -l root
```

```
# If for some valid reason you need to re-enable the account, simply use the -u option.
sudo passwd -u root
```

### 2.6 Secure Shared Memory
One of the first things you should do is secure the shared memory used on the system. If you're unaware, shared memory can be used in an attack against a running service. Because of this, secure that portion of system memory.

Edit /etc/fstab
```
sudo nano /etc/fstab
```

Insert the following line to the bottom of the file and save/close. This sets shared memory into read-only mode.
```
tmpfs    /run/shm    tmpfs    ro,noexec,nosuid    0 0
```

Reboot the node in order for changes to take effect.
```
sudo reboot
```

### 2.7 Install Fail2ban

Fail2ban is an intrusion-prevention system that monitors log files and searches for particular patterns that correspond to a failed login attempt. If a certain number of failed logins are detected from a specific IP address (within a specified amount of time), fail2ban blocks access from that IP address.
```
sudo apt-get install fail2ban -y
```

Edit a config file that monitors SSH logins.
```
sudo nano /etc/fail2ban/jail.local
```

Add the following lines to the bottom of the file.
```
Whitelisting IP address tip: The ignoreip parameter accepts IP addresses, IP ranges or DNS hosts that you can specify to be allowed to connect. This is where you want to specify your local machine, local IP range or local domain, separated by spaces.
# Example
ignoreip = 192.168.1.0/24 127.0.0.1/8

[sshd]
enabled = true
port = <22 or your random port number>
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
# whitelisted IP addresses
ignoreip = <list of whitelisted IP address, your local daily laptop/pc>
```

Save/close file.

Restart fail2ban for settings to take effect.
```
sudo systemctl restart fail2ban
```


### 2.8	Configure your Firewall

The standard UFW firewall can be used to control network access to your node.
With any new installation, ufw is disabled by default. Enable it with the following settings.

Prysm

```
# By default, deny all incoming and outgoing traffic
sudo ufw default deny incoming
sudo ufw default allow outgoing
# Allow ssh access
sudo ufw allow ssh #<port 22 or your random ssh port number>/tcp
# Allow p2p ports
sudo ufw allow 13000/tcp
sudo ufw allow 12000/udp
# Allow eth1 port
sudo ufw allow 30303/tcp
sudo ufw allow 30303/udp
# Enable firewall
sudo ufw enable
```

> **Note**
> It is dangerous to open 3000 / 9090 for Grafana or Prometheus on a VPS/cloud node.

### 2.9	Verify Listening Ports

If you want to maintain a secure server, you should validate the listening network ports every once in a while. This will provide you essential information about your network.

```
sudo ss -tulpn or sudo netstat -tulpn
```
> **Note**
> Further tips can be found here: 
> https://www.ubuntupit.com/best-linux-hardening-security-tips-a-comprehensive-checklist/


## 3. Initial Setup 

### 3.1	Time Sync Check
Run the following command: 
```
timedatectl 
```

:white_check_mark: Check if NTP Service is active.<br>
:white_check_mark: Check if Local time, Time zone, and Universal time are all correct.<br>
:white_check_mark: If NTP Service is not active, run:<br>
```
sudo timedatectl set-ntp on 
```

If you see error message Failed to set ntp: NTP not supported, you may need to install chrony or ntp package. 
> **Note**
> by default, VMs may disable NTP so you may need to find a work-around for your environment.


### 3.2	Create a jwtsecret file

A jwtsecret file contains a hexadecimal string that is passed to both Execution Layer client and Consensus Layer clients, and is used to ensure authenticated communications between both clients.

```
#store the jwtsecret file at /secrets
sudo mkdir -p /secrets
```

```
#create the jwtsecret file
openssl rand -hex 32 | tr -d "\n" | sudo tee /secrets/jwtsecret
```

```
#enable read access
sudo chmod 644 /secrets/jwtsecret
```

### 3.3	Install Execution Client

To process incoming validator deposits from the execution layer (formerly 'Eth1' chain), you'll need to run an execution client as well as your consensus client (formerly 'Eth2'). You can use a third-party service like Infura, but we recommend running your own client to keep the network as decentralized as possible. Go Ethereum is one of the three original implementations (along with C++ and Python) of the Ethereum protocol. It is written in Go, fully open source and licensed under the GNU LGPL v3.

 ![image](https://user-images.githubusercontent.com/33572557/190466176-d9ddd7d5-6ed3-4407-acd1-95c1213a4b0d.png)


Client Comparison Table
Client	Type	CPU Usage	Minimum RAM Usage	Sync Time
Geth	Full	Moderate	4 GB	Moderate
Besu	Full	Moderate	8 GB	Slow
Nethermind	Full	Moderate	16 GB	Fast



## Resources

<details>
  <summary>Knowledge Base</summary>
  Links to aggregators of knowledge with additional information on topics above and more

* ConsenSys: https://consensys.net/knowledge-base/ethereum-2
* BeaconChain: https://kb.beaconcha.in
* Ethhub: https://docs.ethhub.io/ethereum-roadmap/ethereum-2.0/eth-2.0-phases/
* Calculator + resources: https://docs.google.com/spreadsheets/d/15tmPOvOgi3wKxJw7KQJKoUe-uonbYR6HF7u83LR5Mj4/edit#gid=1548910165

</details>

<details>
  <summary>Ethereum 2.0 block explorers</summary> 
  
* Etherscan: https://beaconscan.com
* Beacon Chain: https://beaconcha.in
  
</details>


<details>
  <summary>Validator stats</summary> 
  
* Eth2stats: https://eth2stats.io/medalla-testnet
  
</details>

<details>
  <summary>Ethereum 2.0 client implementations</summary> 
  
* Prysm (Go): https://github.com/prysmaticlabs/prysm
* Lighthouse (Rust) https://github.com/sigp/lighthouse
* Teku (Java): https://github.com/PegaSysEng/teku
* LodeStart (TypeScript): https://github.com/ChainSafe/lodestar
* Trinity (Python): https://github.com/ethereum/trinity

</details>



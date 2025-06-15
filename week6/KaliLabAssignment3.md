# Assignment 3: Penetration Testing with Kali Linux, Metasploit, and Metasploitable2

## Starting Your Kali Linux VM with Vagrant

Before beginning the lab, use the following steps to start and access your Kali Linux virtual machine using Vagrant:

1. Open a terminal and navigate to your Vagrant project directory (where your Vagrantfile is located).
2. Start the VM with:
   ```bash
   vagrant up
   ```
   This command will boot up your Kali Linux VM.
3. Once the VM is running, connect to it with:
   ```bash
   vagrant ssh
   ```
   This command will log you into the Kali Linux VM via SSH, allowing you to run all subsequent commands directly inside the VM.

---

## Section A: Starting Metasploit Framework and Metasploitable 2

### Prerequisites
Ensure Kali Linux and Metasploitable2 are installed and running in a VirtualBox environment. Kali Linux should be able to connect to Metasploitable2 via a private network, which can be verified by `ping` or `ssh`. If networking issues arise on the Metasploitable2 VM, you can set up networking using the following commands:

```bash
sudo ip addr add 192.168.100.200/24 dev eth1
sudo ip link set eth1 up
```
When prompted for a password, use `msfadmin`.

### Start Both VMs
Start both your Kali Linux (Vagrant Install) and Metasploitable2 virtual machines. Verify connectivity by pinging the Metasploitable2 VM from Kali Linux:

```bash
ping 192.168.100.200
```

**Screenshot 1: Both VMs running and connected (ping test)**

![Kali and Metasploitable2 VMs running and ping test](./SS1%20Vagrant%20and%20MS.png)

### Start Metasploit Framework
Start the Metasploit Framework by executing the following command in Kali Linux:

```bash
sudo msfdb init && msfconsole
```

**Screenshot 2: Metasploit Framework successfully started**

![Metasploit Framework started](./SS2%20database%20up.png)

---

## Section B: Use Metasploit Framework to Perform a Port Scan of the Target VM

### Search for Port Scanners
To find all possible scanners, use the Metasploit search command. To refine the results to only port scanners, use:

```bash
search portscan
```

**Screenshot 3: Results of Metasploit search for "portscan"**

![Metasploit portscan search results](./SS3%20Port%20scan.png)

### Select and Configure Port Scanner
Select the TCP port scanner module and configure it to scan the Metasploitable2 VM:

```bash
use auxiliary/scanner/portscan/tcp
set RHOSTS 192.168.100.200
set PORTS 1-1024
```

**Screenshot 4: Port scanner module selected and configured**

![Port scanner module configured](./SS4%20ports%20set.png)

### Run the Port Scan
Initiate the port scan by issuing the following command:

```bash
run
```

**Screenshot 5: Results of the port scan (open TCP ports listed)**

![Port scan results](./SS5%20scan%20result.png)

---

## Questions & Answers

**1. What is the purpose of port scanning from the perspective of a Black Hat hacker?**

From the perspective of a Black Hat hacker, the purpose of port scanning is to discover open ports and services running on a target system. This information helps them identify potential vulnerabilities or entry points that can be exploited to gain unauthorized access, launch attacks, or gather further intelligence for their malicious activities.

**2. What is the purpose of port scanning from the perspective of an Ethical (White Hat) Hacker?**

For an Ethical (White Hat) Hacker, port scanning is a crucial step in the reconnaissance phase of a penetration test. Its purpose is to identify open ports and services on a system to understand the network's attack surface, much like a Black Hat hacker. However, the intent is to proactively discover potential vulnerabilities and misconfigurations before malicious actors do, allowing for these issues to be remediated to improve the system's security posture.

**3. Why did we restrict the scanned ports to 1 through 1024?**

We restricted the scanned ports to 1 through 1024 because these are known as "well-known ports". These ports are typically associated with common services and applications (e.g., HTTP on port 80, FTP on port 21, SSH on port 22, DNS on port 53). Scanning this range provides a quick overview of the most commonly exposed services, which are often the initial targets for reconnaissance and exploitation attempts.

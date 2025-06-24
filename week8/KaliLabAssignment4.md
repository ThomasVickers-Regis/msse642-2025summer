# Assignment 4: Penetration Testing Part 2 – Nessus

## Introduction
Nessus is a powerful vulnerability scanner developed by Tenable, Inc. It is widely used by security professionals to identify vulnerabilities, misconfigurations, and compliance issues in systems and networks. Nessus is available at [https://www.tenable.com/products/nessus](https://www.tenable.com/products/nessus) and offers a free "Essentials" version for students and small environments.

## Big Picture: Where Nessus Fits in Penetration Testing
Nessus is primarily used during the **Vulnerability Scanning** phase of the penetration testing process. According to the Singh book (Chapter 8, p. 257), this phase follows information gathering and scanning, and involves identifying known vulnerabilities in discovered services and systems. Nessus automates this process, providing detailed reports on potential weaknesses that attackers could exploit.

## Lab: Installing and Using Nessus in the Kali/Metasploitable2 Lab

### Prerequisites
- Kali Linux and Metasploitable2 VMs running in VirtualBox
- Private network connectivity between Kali and Metasploitable2 (verify with `ping`)

### Step-by-Step Guide

#### 1. Start Your Kali Linux VM with Vagrant
```bash
cd /path/to/your/vagrant/project
vagrant up
vagrant ssh
```

#### 1.5. Ensure Metasploitable2 Network Connectivity
If you have trouble connecting from Kali to Metasploitable2, ensure both VMs are running and networked properly. You may need to manually configure the network interface on Metasploitable2:

**On Metasploitable2 VM:**
```bash
# Assign a static IP to the second network interface (eth1)
sudo ip addr add 192.168.100.200/24 dev eth1
sudo ip link set eth1 up
```
- When prompted for a password, use: `msfadmin`

**On Kali Linux VM:**
- (Recommended) Clear any previous IPs from eth1 before assigning the new one:
```bash
sudo ip addr flush dev eth1
sudo ip addr add 192.168.100.100/24 dev eth1
sudo ip link set eth1 up
```
- Test connectivity with:
```bash
ping 192.168.100.200
```
- You should see replies if the network is set up correctly.

**VirtualBox Network Adapter Settings (Kali and Metasploitable2):**
1. **Shut down both VMs.**
2. In VirtualBox Manager, select each VM and go to **Settings > Network**.
3. For **Adapter 2**:
   - Check **Enable Network Adapter**
   - Set **Attached to:** `Host-only Adapter`
   - Set **Name:** (e.g., `vboxnet0`) — must be the same for both VMs
4. Start both VMs again.

**Notes:**
- Both VMs should be set to use a "Host-only Adapter" or "Internal Network" in VirtualBox for the private network.
- The IP `192.168.100.200` is commonly used for Metasploitable2 in these labs.
- Assign Kali an IP like `192.168.100.100/24` on its eth1 interface to match the subnet.

#### 2. Install Nessus (if not already installed)
```bash
# Download the official Nessus Debian package using curl
curl --request GET \
  --url 'https://www.tenable.com/downloads/api/v2/pages/nessus/files/Nessus-10.8.4-debian10_amd64.deb' \
  --output 'Nessus-10.8.4-debian10_amd64.deb'

# Verify the file type and size
file Nessus-10.8.4-debian10_amd64.deb
ls -lh Nessus-10.8.4-debian10_amd64.deb
# The file type should be: Debian binary package
# The file size should be tens of MB (not a few KB)

# Install Nessus
sudo dpkg -i Nessus-10.8.4-debian10_amd64.deb

# Start and enable Nessus service
sudo systemctl start nessusd
sudo systemctl enable nessusd

# Check Nessus service status
sudo systemctl status nessusd
# You should see 'active (running)' in the output
# If not, troubleshoot before proceeding
```

#### 3. Access Nessus Web Interface
- Open a browser on your host machine.
- Go to: `https://localhost:8834/` (or use the VM's IP if needed)
- Complete the setup (create an account, register for a free activation code at [Tenable](https://www.tenable.com/products/nessus/nessus-essentials), and enter it).

#### 3.5. (Optional) Set Up Port Forwarding for Browser Access from Host
If your Kali VM uses NAT networking and you want to access Nessus from your host machine's browser, set up port forwarding in VirtualBox:

1. **Shut down your Kali VM.**
2. In VirtualBox Manager, select your Kali VM and go to **Settings > Network**.
3. For the adapter set to **NAT** (usually Adapter 1), click **Advanced** > **Port Forwarding**.
4. Add a new rule:
   - **Name:** Nessus
   - **Protocol:** TCP
   - **Host IP:** 127.0.0.1 (or leave blank)
   - **Host Port:** 8834
   - **Guest IP:** (leave blank or use Kali's NAT IP, e.g., 10.0.2.15)
   - **Guest Port:** 8834
5. Click **OK** to save and start your Kali VM.

Now, on your host machine, open a browser and go to:
```
https://localhost:8834
```
This will forward traffic from your host's port 8834 to the Kali VM's port 8834, allowing you to access the Nessus web interface.

**Alternatively:**
- You can always open a browser **inside the Kali VM** and go to `https://localhost:8834` directly.

#### 4. Scan Metasploitable2 with Nessus
- In Nessus, create a **New Scan**.
- Choose **Basic Network Scan**.
- Set the target as the Metasploitable2 IP (e.g., `192.168.100.200`).
- Save and launch the scan.
- Wait for the scan to complete, then review the results.

---

### Nessus Essentials: Registration and Activation Code
To use Nessus Essentials, you must register with a free activation code (license key). This is required to enable plugin updates and full scanning functionality.

1. **Get a Free Activation Code:**
   - Visit [Tenable Nessus Essentials](https://www.tenable.com/products/nessus/nessus-essentials) and fill out the form to receive your activation code by email. (There is a student license)

2. **Enter the Activation Code During Setup:**
   - The Nessus web interface will prompt you for the activation code during the initial setup.
   - If you missed this step or need to re-enter the code, you can register from the command line:
     ```bash
     sudo /opt/nessus/sbin/nessuscli fetch --register <your-activation-code>
     ```
   - Replace `<your-activation-code>` with the code you received from Tenable.

3. **After Registration:**
   - Once registered, Nessus will download the plugin set. This may take several minutes.
   - You must complete this step before you can perform scans.

---

### Offline Registration (Challenge/Response)
If your Nessus installation prompts you for a challenge code (for example, if you are registering offline):

1. **Copy the challenge code** shown in the Nessus web interface or from the CLI.
2. Enter challenge code with license key and this hould generate a license key block.
3. **Paste the entire license key block** (including the BEGIN and END lines) into the license key field in Nessus when prompted.

This process allows you to activate Nessus without direct internet access on the VM.

---

### Quick Fix: Nessus Shows "No Plugins" or Limited Functionality
If Nessus reports that it has no plugins or limited functionality, try this quick fix:

1. **Update Only the Plugins**
   ```bash
   sudo /opt/nessus/sbin/nessuscli update --plugins-only
   sudo systemctl restart nessusd
   ```
   This will refresh the plugin set and restart Nessus. Wait a few minutes, then refresh the web interface.

---

### Lab: Installing and Using Nessus in the Kali/Metasploitable2 Lab
Nessus is not included in the default Kali Linux installation, but it is easy to install using the `.deb` package from Tenable's website. After installation and setup, Nessus is accessed via a web browser. In my lab, I scanned the Metasploitable2 VM from Kali Linux. The scan identified numerous vulnerabilities, including outdated services and default credentials, demonstrating how attackers could exploit these weaknesses.

**Screenshot: Nessus scan results for Metasploitable2**

Host Discovery Scan:
![Nessus Scan Results 1](SS1%20host%20discovery%20scan.png)

Vulnerability Scan:
![Nessus Scan Results 2](SS2%20Vulnerability%20scan.png)

Vulnerability Scan List:
![Nessus Scan Results 3](SS3%20Vulnerability%20List.png)

### Conclusion
Nessus is an essential tool for vulnerability assessment in penetration testing. It automates the process of finding known vulnerabilities, helping both attackers and defenders understand the security posture of a system. In my lab, Nessus quickly identified critical issues in Metasploitable2, highlighting the importance of regular vulnerability scanning in any security program.

### References
- Singh, Glen (2019). Learn Kali Linux 2019. Packt. [O'Reilly Online](https://learning.oreilly.com/library/view/learn-kali-linux/9781789611809/)
- Tenable Nessus: https://www.tenable.com/products/nessus
- Kali Linux Documentation: https://www.kali.org/docs/
- Metasploitable2: https://sourceforge.net/projects/metasploitable/


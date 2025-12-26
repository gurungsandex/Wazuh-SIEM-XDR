# WazuhProject  
This home-lab project helps build a realistic, SOC-style lab at home or in VMs.  
This home lab project demonstrates how to host a **Wazuh Server** on an Ubuntu server and how to enroll agents on other machines/VMs.  

I want to make this project as simple as possible!  

This gives a working mini SOC home lab!

---

## ✅ Advantages of this project
- 💰 Free of cost  
- 🖥️ Easy to learn & implement  
- 🚀 Beginner-friendly  

---

## 🔹 What is Wazuh? 
Wazuh is an **open-source security monitoring platform (SIEM + XDR)** that provides:  
- Agent-based endpoint monitoring  
- Log analysis & alerting  
- File integrity monitoring (FIM)  
- Vulnerability detection  
- Threat detection & response  

It’s widely used in security operations centers (SOCs) for real-time visibility and defense.  

---

## 🔹 Project Expectation
In this project, I will:  
1. Install **Wazuh Server** on an Ubuntu Server VM.  
2. Deploy a **Wazuh Agent** on a Kali Linux VM.  
3. Connect the agent to the server and verify successful enrollment.  
4. Demonstrate alerts to confirm communication between server and agent(s).  

---

## 🔹 Lab Environment (VirtualBox on macOS)
- **Host machine**: MacBook (running VirtualBox)  
- **VM 1**: Ubuntu Server → Wazuh Server  
- **VM 2**: Kali Linux → Wazuh Agent  

---

## 🛠️ Wazuh Server Installation on Ubuntu Server
**Step 1**: Update packages and run the Wazuh installer:  
            
            sudo apt update && sudo apt upgrade -y
            
            curl -sO https://packages.wazuh.com/4.13/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
            
Step 2: After installation, it will generate a username and password to access Wazuh server dashboard.
<img width="1025" height="466" alt="wazuh server installation" src="https://github.com/user-attachments/assets/552f49ce-6298-49a4-92f0-75d616e3d38c" />

Step 3: Find the server IP address of Ubuntu server (Wazuh server is hosted on Ubuntu), and use this IP to access the Wazuh dashboard in the browser. 
<img width="1017" height="630" alt="server ip address" src="https://github.com/user-attachments/assets/e402632a-f8a5-4372-a3c2-70d531f72a5c" />

Step 4: Login with the generated username and password to verify the dashboard is working.
<img width="993" height="573" alt="wazuh dashboard" src="https://github.com/user-attachments/assets/4c3da5a3-0ae9-47e2-b033-1754eaf66551" />

---------------------------------------------------------------------------------------------------------------------------------------------
## 🖥️ Wazuh Agent Deployment on Kali Linux
Step 1: From the Wazuh Dashboard, go to:
👉 Deploy new agent
Select agent OS type = Kali Linux (Debian-based)
Server address = Ubuntu server IP address.
It will generate commands to deploy agent. 
<img width="1093" height="670" alt="agent deployment1" src="https://github.com/user-attachments/assets/74eb35ff-9f8b-4276-8bf2-ec5d7eebc092" />

Step 2: Run the commands on Kali terminal 
<img width="1259" height="668" alt="agent deployment2" src="https://github.com/user-attachments/assets/fac002b8-7224-4763-8fb8-4457c6f0b8fe" />

<img width="1255" height="685" alt="agent deployment3" src="https://github.com/user-attachments/assets/49353b55-7356-4533-a1be-4a2a7eca10c7" />

Step 3: Check the Wazuh Dashboard to confirm the agent is enrolled and shows status active.
<img width="1264" height="511" alt="agent deploy5" src="https://github.com/user-attachments/assets/c1ba6783-ba69-48b8-a1e5-497b281daddf" />

---------------------------------------------------------------------------------------------------------------------------------------------
## Playing with Alerts
## Privilege Escalation Demo

In this demo, I’ll show how Wazuh detects failed privilege-escalation attempts (wrong sudo password) and how those events travel from the agent to the server. This is a simple way to prove the agent ↔ server communication chain.
1. On the Kali agent, I intentionally entered the wrong sudo password several times to trigger authentication failures.
<img width="865" height="204" alt="login attempt" src="https://github.com/user-attachments/assets/510987dc-e83c-4446-9355-3e00b6b128cd" />

2. These failed attempts show up in the Wazuh alerts, proving the agent is successfully reporting to the server. 
<img width="898" height="631" alt="login attempt3" src="https://github.com/user-attachments/assets/70b5a7b2-e413-472b-afa5-25469be90349" />

---------------------------------------------------------------------------------------------------------------------------------------------
## File Integrity Monitoring
In this demo, I will show how changes made on the agent are detected by Wazuh server, proving agent → server communication.
1. Before everything can function properly, we need to do some essential configurations to enable the system to work correctly. Edit the agent’s configuration file: /var/ossec/etc/ossec.conf. In the "File Integrity Monitoring" section of ossec.conf file, enable the alerting/monitoring for the paths you want to watch (e.g., /root, /etc/hosts).

            sudo nano /var/ossec/etc/ossec.conf
   
<img width="992" height="245" alt="file integrity 1" src="https://github.com/user-attachments/assets/1271ade0-8608-4ecc-a106-0b627c6cc168" />

2. After editing, save the file and restart the agent so the new FIM settings take effect.
   
            sudo systemctl restart wazuh-agent

3. Now, on the monitored machine, create and remove files (or edit files) in the monitored path to generate FIM events.
<img width="732" height="510" alt="file integrity 2" src="https://github.com/user-attachments/assets/c063dcae-d432-49e1-b517-1cd3c1b001a1" />

4. Now, view alerts on the Wazuh server. The alerts should be shown for the file creations/deletions performed.
<img width="1203" height="643" alt="file integrity 3" src="https://github.com/user-attachments/assets/a28243b1-2e05-4a6d-bdf3-4938336fb77c" />   

---------------------------------------------------------------------------------------------------------------------------------------------
## SSH Brute‑Force Attack from an External Machine

In this demonstration, I show how an SSH brute‑force attack is detected in Wazuh Server.
I simulate an attack from my host machine against a Linux agent running in a virtual machine.

## Steps:

Find the IP address of the agent (virtual machine).

From the host machine, attempt to connect to the agent using SSH.

Enter an incorrect username or password multiple times.

<img width="575" height="180" alt="ssh attack 1" src="https://github.com/user-attachments/assets/d5f15086-1d01-4617-a9d2-7c15f54b477d" />


Wazuh detects the failed login attempts and logs the event in the Wazuh server dashboard.
This confirms that Wazuh is successfully monitoring and detecting external SSH brute‑force attempts.
<img width="1133" height="636" alt="Screenshot 2025-12-25 at 5 04 35 PM" src="https://github.com/user-attachments/assets/67e4f252-ce5a-4e75-bc13-89f3f46a46e5" />

In this type of brute‑force attack, incident responders such as SOC analysts observe log, the **source IP address** that attempted to log in to the system and other details in depth. Since the login attempts were unsuccessful and the attacker was unable to access the targeted machine, the appropriate containment action is to **block the attacker’s IP address** using security controls such as a firewall or intrusion prevention solution.

## MITRE ATT&CK framework mapping
We can also map the detected log to the MITRE ATT&CK framework, which helps identify the attacker’s behavior. In this case, the activity/MITRE technique is classified as Brute Force, with ID T1110, under the Credential Access tactic. Mapping security events to the MITRE ATT&CK framework is important because it provides a standard way to understand and describe attacks.
MITRE mapping is used to: 
            Standardize incident classification, 
            Improve detection and response
            Identify attack patterns and trends
            Support threat hunting
            Meet compliance and reporting requirements

## Security Measures for SSH BruteForce Attack

## 🔐 Preventive Controls

            Disable password‑based SSH login and use SSH key authentication.

            Restrict SSH access to specific IP addresses.

            Change the default SSH port.

            Enforce strong password policies.

## 🛡️ Detection & Response

            Enable account lockout after multiple failed login attempts.

            Use tools like fail2ban to automatically block attacking IPs.

            Monitor authentication logs continuously using a SIEM (like Wazuh).

## 📋 Best Practices

            Regularly review SSH access logs.

            Apply system updates and patches.

            Follow the principle of least privilege for user accounts.



This Wazuh home lab is an ongoing project. I will continue expanding and refining this lab environment by adding more attack scenarios, detections, and incident response use cases.


















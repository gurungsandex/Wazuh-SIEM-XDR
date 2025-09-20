# WazuhProject  
This home-lab project helps build a realistic, SOC-style lab at home or in VMs.  
This home lab project demonstrates how to host a **Wazuh Server** on an Ubuntu server and how to enroll agents on other machines/VMs.  

I want to make this project as simple as possible!  

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

Step 3: Find the server IP address of Ubuntu server (Wazuh server is hosted on Ubuntu), and use this IP to access the Wazuh dashboard in your browser. 
<img width="1017" height="630" alt="server ip address" src="https://github.com/user-attachments/assets/e402632a-f8a5-4372-a3c2-70d531f72a5c" />

Step 4: Login with the generated username and password to verify the dashboard is working.
<img width="993" height="573" alt="wazuh dashboard" src="https://github.com/user-attachments/assets/4c3da5a3-0ae9-47e2-b033-1754eaf66551" />

## 🖥️ Wazuh Agent Deployment on Kali Linux
Step 1: From the Wazuh Dashboard, go to:
👉 Deploy new agent
Select agent OS type = Kali Linux (Debian-based)
Server address = Ubuntu server IP address 
<img width="1093" height="670" alt="agent deployment1" src="https://github.com/user-attachments/assets/74eb35ff-9f8b-4276-8bf2-ec5d7eebc092" />

Step 2: Run the commands on Kali terminal 
<img width="1259" height="668" alt="agent deployment2" src="https://github.com/user-attachments/assets/fac002b8-7224-4763-8fb8-4457c6f0b8fe" />

<img width="1255" height="685" alt="agent deployment3" src="https://github.com/user-attachments/assets/49353b55-7356-4533-a1be-4a2a7eca10c7" />

Step 3: Check the Wazuh Dashboard to confirm the agent is enrolled and shows status active.
<img width="659" height="588" alt="agent deploy4" src="https://github.com/user-attachments/assets/6b21aa11-6b27-4bea-95d7-639704c160f0" />

<img width="1264" height="511" alt="agent deploy5" src="https://github.com/user-attachments/assets/c1ba6783-ba69-48b8-a1e5-497b281daddf" />

## Playing with Alerts
            Loading........

            

## 📌 Project Outcome

✅ Wazuh Server running on Ubuntu VM

✅ Kali Linux agent enrolled successfully

✅ Communication verified through alerts


This gives you a working mini SOC home lab!



## 🚀 Next Steps

Add more agents (Windows, other Linux VMs)

Enable log collection from services (SSH, web servers)

Configure File Integrity Monitoring (FIM)

Create custom detection rules


I will keep working on similar projects (SIEM, SOC labs, networking, detection rules) and share them here.
💡 If you try this project, share your results — I’d love to see how you build on it!













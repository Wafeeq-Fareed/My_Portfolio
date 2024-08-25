# Cybersecurity Project: SIEM Configuration, Active Directory, and Brute Force Testing
## Overview
This project is a comprehensive three-phase cybersecurity setup aimed at enhancing network security and testing the robustness of a system against common attack vectors. The project involved configuring a Security Information and Event Management (SIEM) system, setting up and securing an Active Directory environment, and conducting brute force attacks using Kali Linux tools.

## Phase 1: SIEM Configuration with Splunk
### Objective
To set up a Splunk server for monitoring network and endpoint activity, enabling real-time security event analysis.

### Setup Details
Environment:
Virtualization: VirtualBox
Operating System: Ubuntu 22.04 Server
Network: 192.168.10.0/24
Splunk Server IP: 192.168.10.10/24

### Configuration Steps
1. Splunk Server Setup:
- Installed Splunk Enterprise on an Ubuntu 22.04 server hosted in VirtualBox.
- Configured the server to operate within the 192.168.10.0/24 network.

2. Target Machine Configuration:

- Set up a Windows 10 machine, named `target-pc`.
- Configured the IP address to 192.168.10.100 with DNS set to 8.8.8.8.

3. Installing and Configuring Splunk Universal Forwarder:
- Installed the Splunk Universal Forwarder on `target-pc`.
- Configured Sysmon for detailed event logging.
- Added a new endpoint index configuration in inputs.conf located in the \etc\system\local directory, enabling Splunk to capture and analyze endpoint activity.

4. Finalizing the Setup:
- Restarted the splunkuniversalforwarder service to apply changes.
- Accessed the Splunk dashboard via http://192.168.10.10:8000 and performed additional minor configurations to ensure the system was fully operational.

### Outcome
The Splunk server was successfully set up and integrated with the Windows 10 machine, providing a real-time monitoring dashboard for endpoint activities. This configuration allows for proactive threat detection and response.

## Phase 2: Active Directory Configuration
### Objective
To set up and configure an Active Directory Domain Services (ADDS) environment using Windows Server 2022, enabling centralized management of users and devices within the network.

### Setup Details
Environment:
Operating System: Windows Server 2022
Network: 192.168.10.0/24
Server IP: 192.168.10.7
Target Machine: `target-pc` with IP 192.168.10.100
### Configuration Steps
1. Windows Server Installation:
- Downloaded and loaded the Windows Server 2022 ISO image into a virtual machine.
- Booted up the virtual machine and performed the initial configuration.
- Named the server `ADDS` and assigned it a static IP of 192.168.10.7.

2. Active Directory Domain Services Setup:
- Accessed the Server Manager and navigated to Manage > Add Roles and Features.
- Selected and installed the Active Directory Domain Services (ADDS) role.
- Launched the Active Directory Domain Services Configuration Wizard to create a new forest.
- Set the root domain name and configured a Directory Services Restore Mode (DSRM) password.

3. User Profiles and Organizational Units:

- Once the domain server was active, created new user profiles:
- In Server Manager > Tools > Active Directory Users and Computers, right-clicked on the domain server to add a new Organizational Unit (OU) and named it HR.
- Created a new user, John Britto, in the default OU with the username Britto.
- Added another OU named IT and created a user, Joseph Chacko, with the username Jos.
- Configured both accounts with strong passwords.

4.Configuring `target-PC` to Join the Domain:
- On `target-pc`, changed the DNS setting from 8.8.8.8 to the server IP, 192.168.10.7, to allow the device to connect to the Active Directory Domain Services.
- Opened System Properties on `target-pc`, navigated to Advanced system settings > Computer Name tab, and changed the workgroup to the domain MyServ.local.
- After entering administrator credentials, `target-pc` successfully joined the domain.

5. Domain Access Verification:
- Restarted `target-pc` and logged in using the newly created user accounts, John Britto and Joseph Chacko, verifying that the accounts were accessible within the domain environment.

### Outcome
The Active Directory Domain Services were successfully configured, allowing centralized management of users and devices. The `target-pc` was successfully joined to the domain, demonstrating the functional ADDS environment.

## Phase 3: Brute Force Attack Simulation and Monitoring with Splunk

### Objective
To simulate a brute force attack on the Active Directory using Kali Linux and monitor the attack events in real-time using Splunk.

### Setup Details

- **Environment:**
  - **Attacker Machine:** Kali Linux
  - **Target Machine:** `target-pc` with IP 192.168.10.100
  - **User Account Targeted:** Britto

### Configuration Steps

1. **Preparing Kali Linux:**
   - Updated and upgraded the Kali Linux system:
     ```bash
     sudo apt-get update && sudo apt-get upgrade -y
     ```
   - Created a new directory for the project:
     ```bash
     mkdir ad-project
     ```
   - Installed the Crowbar tool for brute force attacks:
     ```bash
     sudo apt-get install -y crowbar
     ```

2. **Preparing the Password List:**
   - Navigated to the wordlists directory to access preloaded brute force passwords:
     ```bash
     cd /usr/share/wordlists
     ```
   - Extracted the `rockyou.txt` file:
     ```bash
     sudo gunzip rockyou.txt
     ```
   - Copied `rockyou.txt` to the `ad-project` directory:
     ```bash
     cp rockyou.txt ~/ad-project/
     ```
   - Extracted the first 20 entries from `rockyou.txt` to create a smaller password list:
     ```bash
     head -n 20 rockyou.txt > passwords.txt
     ```
   - Edited the `passwords.txt` file to include Britto’s actual password:
     ```bash
     nano passwords.txt
     ```

3. **Configuring Remote Desktop on Target-PC:**
   - On `target-pc`, opened **System Properties** and navigated to **Advanced system settings > Remote** tab.
   - Enabled Remote Desktop and added the user Britto for remote access.

4. **Executing the Brute Force Attack:**
   - Accessed Crowbar on Kali and executed the brute force attack:
     ```bash
     crowbar -b rdp -u britto -C passwords.txt -s 192.168.10.100/32
     ```
   - The command initiated a brute force attack on Britto’s account, ultimately unlocking it after successful password discovery.

5. **Monitoring the Attack with Splunk:**
   - Logged into the Splunk dashboard via `http://192.168.10.10:8000`.
   - Searched for the brute force events using the following query:
     ```spl
     index=endpoint eventcode=4625
     ```
   - The results displayed the failed login attempts (Event Code 4625), indicating the brute force attack on Britto’s account.

### Outcome
The brute force attack was successfully executed using Crowbar, and the corresponding security events were accurately captured and displayed in Splunk. This demonstrated the ability to detect and monitor brute force attacks in real-time using SIEM tools.


## Project Summary

This cybersecurity project involved a three-phase setup to enhance network security and simulate attack scenarios for monitoring and defense.

**Phase 1: SIEM Configuration with Splunk**  
A Splunk server was configured on an Ubuntu 22.04 virtual machine within a local network. The server was integrated with a Windows 10 machine (`target-pc`) using Splunk Universal Forwarder and Sysmon, enabling real-time monitoring of endpoint activities through the Splunk dashboard.

**Phase 2: Active Directory Configuration**  
A Windows Server 2022 virtual machine was set up as an Active Directory Domain Controller. User profiles and organizational units were created, and the `target-pc` was successfully joined to the domain, allowing centralized user and device management.

**Phase 3: Brute Force Attack Simulation and Monitoring**  
Using Kali Linux, a brute force attack was simulated on the `target-pc`'s user account (Britto) using the Crowbar tool. The attack was monitored in real-time via the Splunk dashboard, showcasing the system's ability to detect and log security events.

This project demonstrated the integration of SIEM tools, Active Directory management, and the importance of monitoring for potential security breaches.


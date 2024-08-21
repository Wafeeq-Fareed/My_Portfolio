## SIEM DEPLOYMENT USING ELK STACK

## Project Overview
This project involves deploying and configuring an ELK (Elasticsearch, Logstash, Kibana) Stack SIEM solution to monitor and analyze network traffic. The solution was implemented on a virtual Ubuntu agent, using Kibana for real-time data visualization and analysis.

## Objectives
- Deploy an ELK Stack for centralized log management and analysis.
- Add virtual agent (Ubuntu 22.04 LTS) to the Fleet.
- Monitor network traffic in real-time using Kibana.
- Create dashboards with specific fields from Discover in Kibana

## Technologies Used
- **Operating System**: Ubuntu 22.04 LTS
- **ELK Stack**: Elasticsearch, Logstash, Kibana
- **Virtualization**: VirtualBox
- **Cloud Deployment**: Google Cloud.

## Deployment Steps

### 1. Set Up Ubuntu Virtual Machine
- Download Ubuntu 22.04 LTS ISO file from [www.releases.ubuntu.com](https://releases.ubuntu.com/22.04/?_gl=1*31l1ob*_gcl_au*MTg3NTc1MjcuMTcyNDEzNzA0Nw..&_ga=2.135338929.1635614044.1724137043-1911747749.1724137043)
- Create new Ubuntu virtual machine using the ISO file downloaded and configure user settings.

### 2. Access ELK Stack
- On the host machine or in a separate virtual machine log into Elasticsearch, Logstash, and Kibana stack using the official website.
- Create a trial account to deploy ELK in desired cloud platform and geographical location.

### 3. Configure Fleet
- Set up an agent using management option - <u>Fleet</u>.
- Click on <u>Add Agent</u> and provide agent policy
- Choose enroll in the Fleet. 
- Copy and execute the curl command on the virtual Ubuntu Terminal previously installed.

### 4. Set Up Kibana
- Once the agent is available on Fleet. 
- Deploy Kibana and open up <u>Discover</u> from Kibana menu.
- Use the available parameteres to create custom dashboards to monitor network traffic.

## Results
- Successfully monitored and visualized network traffic in real-time.
- Detected anomalies in traffic patterns and generated alerts.
- Created a dashboard with key performance indicators (KPIs) for network security.

## Challenges and Solutions
- **Challenge**: Installing ELK leads to high resource usage on a limited hardware.
- **Solution**: Deployed the entire stack on Google Cloud, effectively mitigating limited hardware constraints by leveraging cloud-based infrastructure for scalability and performance.

## Future Improvements
- Integrate additional data sources such as firewall logs, IDS/IPS logs and Sysmon logs(For Windows).
- Implement LLAMA LLMs for predictive analysis integrating with a SOAR for automated predictive responses.

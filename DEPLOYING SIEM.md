## ELK STACK SIEM DEPLOYMENT

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
- **Cloud Deployment**: The SaaS service is deployed in Google Cloud.

## Deployment Steps

### 1. Set Up Ubuntu Virtual Machine
- Install Ubuntu 22.04 LTS on VirtualBox using ISO file from https://releases.ubuntu.com/22.04/?_gl=1*31l1ob*_gcl_au*MTg3NTc1MjcuMTcyNDEzNzA0Nw..&_ga=2.135338929.1635614044.1724137043-1911747749.1724137043.
- Configure network settings to enable monitoring.

### 2. Install ELK Stack
- Install Elasticsearch, Logstash, and Kibana using the official repositories.
- Configure Elasticsearch for optimal performance.

### 3. Configure Logstash
- Set up Logstash to parse and forward logs from the Ubuntu VM.
- Implement custom filters for network traffic logs.

### 4. Set Up Kibana
- Deploy Kibana for data visualization.
- Create custom dashboards to monitor network traffic.

## Results
- Successfully monitored and visualized network traffic in real-time.
- Detected anomalies in traffic patterns and generated alerts.
- Created a dashboard with key performance indicators (KPIs) for network security.

## Challenges and Solutions
- **Challenge**: High resource usage by Elasticsearch on limited hardware.
- **Solution**: Optimized Elasticsearch configurations and allocated additional resources to the VM.

## Future Improvements
- Integrate additional data sources such as firewall logs.
- Implement machine learning algorithms for predictive analysis.

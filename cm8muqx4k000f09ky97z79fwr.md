---
title: "Setup Grafana in Windows"
datePublished: Mon Mar 24 2025 09:16:09 GMT+0000 (Coordinated Universal Time)
cuid: cm8muqx4k000f09ky97z79fwr
slug: setup-grafana-in-windows
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742803529274/89068079-89e9-4b81-a8e3-713541b508ee.png
tags: devops, grafana

---

Monitoring Windows Server performance using Grafana involves several steps, including setting up data collection, configuring Grafana, and creating dashboards. Below is a step-by-step guide to help you set up monitoring for a Windows Server using Grafana:

### **Step 1: Prerequisites**

1. **Windows Server**: Ensure you have administrative access to the server you want to monitor.
    
2. **Grafana**: Install Grafana on a machine (can be the same server or a separate machine).
    
3. **Prometheus**: Install Prometheus as the data source for Grafana.
    
4. **Windows Exporter**: Install the Windows Exporter on the Windows Server to collect performance metrics.
    

### **Step 2: Install Windows Exporter on the Windows Server**

The Windows Exporter collects performance metrics from the Windows Server and exposes them in a format that Prometheus can scrape.

1. Download the latest release of the Windows Exporter from the [GitHub releases page](https://github.com/prometheus-community/windows_exporter/releases).
    
2. Extract the `.msi` file and install it on the Windows Server.
    
3. During installation, you can select which metrics to collect (e.g., CPU, memory, disk, network).
    
4. After installation, the exporter will run as a service and expose metrics on `http://<server-ip>:9182/metrics`.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742804202701/a59f9955-aaa2-4b71-82f4-3eda7cef9aac.png align="center")

### **Step 3: Install and Configure Prometheus**

Prometheus will scrape the metrics exposed by the Windows Exporter.

1. Download Prometheus from the [official website](https://prometheus.io/download/).
    
2. Extract the files and configure the `prometheus.yml` file to scrape metrics from the Windows Exporter:
    
3. Edit the `prometheus.yml` file and save the file
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742804519190/57f5373a-badd-4788-a579-427ed722611d.png align="center")

4. Start Prometheus:
    
    open CMD as Administartor and locate the location where Promethues is stored
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742804712038/571e758b-217d-41dd-afe6-67558afda961.png align="center")
    
    Run this command —→ prometheus.exe --config.file=prometheus.yml
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742804815520/afbfa2cd-a519-4503-b9c6-759ebaa245ee.png align="center")
    
5. Verify that Prometheus is scraping data by visiting [`http://localhost:9090`](http://localhost:9090) and querying for a metric: windows\_memory\_available\_bytes
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742806350122/78c95b85-5ae8-430f-bafc-3b8cc75c18a2.png align="center")
    

### **Step 4: Install Grafana**

Grafana will visualize the metrics collected by Prometheus.

1. Download Grafana from the [official website](https://grafana.com/grafana/download).
    
2. Install Grafana on your machine (Windows or Linux).
    
3. Start Grafana and access the web interface at `http://localhost:3000`.
    
4. Log in with the default credentials (`admin/admin`) and change the password.
    

### **Step 5: Add Prometheus as a Data Source in Grafana**

1. In Grafana, go to **Configuration &gt; Data Sources**.
    
2. Click **Add data source** and select **Prometheus**.
    
3. Set the URL to [`http://localhost:9090`](http://localhost:9090) (or the address where Prometheus is running).
    
4. Click **Save & Test** to ensure the connection is successful.
    

### **Step 6: Create a Dashboard in Grafana**

1. Go to **Dashboards &gt; New Dashboard**.
    
2. Add a new panel and select the Prometheus data source.
    
3. Use Prometheus queries to visualize metrics. For example:
    
    * CPU Usage: `rate(windows_cpu_time_total[1m])`
        
    * Memory Usage: `windows_memory_available_bytes`
        
    * Disk I/O: `rate(windows_logical_disk_read_bytes_total[1m])`
        
4. Customize the panel with graphs, gauges, or other visualization types.
    
5. Save the dashboard.
    

## final look of your windows performance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742806783239/807fbee3-8fd7-4d2e-aaa8-6195d849c523.png align="center")